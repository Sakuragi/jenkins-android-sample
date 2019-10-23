pipeline{
    agent {
        docker {
            image 'javiersantos/android-ci:28.0.3'
        }
    }
    stages {
        stage('checkout code'){
             steps {
                sh 'echo checkout code'
             }
        }
        stage('Clean') {
            steps {
                sh 'yes | /sdk/tools/bin/sdkmanager --licenses'
                sh 'chmod 777 ./gradlew'
                sh './gradlew clean'
                sh 'echo init finished'
            }
        }
        stage('Build'){
            steps{
                script {
                   if (env.buildType == 'release') {
                       sh './gradlew assembleRelease'
                   } else {
                       sh './gradlew assembleDebug'
                   }
                }
            }
        }
        stage('PrintApk') { 
            steps {
                sh 'echo =========Build OK========'
                sh 'echo ${EMAIL}'
            }
        }
    }
    post {
        success {
            emailext (
                subject: "SUCCESSFUL: Job '${env.JOB_NAME} '",
                body: "SUCCESSFUL",
                to: "${EMAIL}"
            )
        }
        failure {
            emailext (
                subject: "FAILED: Job '${env.JOB_NAME}'",
                body: """<p>FAILED</p>""",
                to: "${EMAIL}"
            )
        }
    }

}