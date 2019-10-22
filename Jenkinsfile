pipeline{
    agent {
        docker {
            image 'javiersantos/android-ci:28.0.3'
        }
    }
    stages {
        stage('checkout code'){
            echo "检出代码"
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
             if(env.buildType=='release'){
                  sh './gradlew assembleRelease'
              }else{
                  sh './gradlew assembleDebug'
              }
        }
        stage('PrintApk') { 
            steps {
                sh 'echo =========Build OK========'
            }
        }
    }
}