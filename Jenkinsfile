pipeline{
    agent {
        docker {
            image 'javiersantos/android-ci:28.0.3'
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'chmod 777 ./gradlew'
                sh './gradlew clean' 
                sh './gradlew assembleRelease' 
            }
        }
        stage('PrintApk') { 
            steps {
                sh 'ls -all apk/ && echo =========Build OK========'
            }
        }
    }
}