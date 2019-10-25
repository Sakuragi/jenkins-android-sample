pipeline{
    agent {
        docker {
            image 'jenkins-android:1.0.0'
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

}