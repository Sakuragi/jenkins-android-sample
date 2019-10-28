pipeline{
    agent {
        docker {
            image 'jenkins-android:1.0.0'
            args  '-v /tmp/gradlecache:/root'
        }
    }
    stages {
        stage('checkout code'){
             steps {
                sh 'ls -all  /'
                sh 'ls /var/jenkins_home/workspace/'
                sh 'git config user.name'
                sh 'git clone git@dev-gitlab.getui.net:lijm/PackShellDemo.git'
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