node{
    stages {
        agent {
            docker {
                image 'javiersantos/android-ci:28.0.3'
            }
        }
        stage('checkout code'){
             if (env.buildType == 'release') {
                 echo './gradlew assembleRelease'
             }
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
            }
        }
    }
}