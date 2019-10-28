pipeline{
    agent {
        docker {
            image 'allbears/jenkins-android:1.0.1'
            args  '-v /tmp/gradlecache:/root'
        }
    }
    environment {
       USER_NAME = 'lijm'
       USER_EMAIL= 'lijm@getui.com''
    }
    stages {
        stage('checkout code'){
             steps {
                sh 'git config --global user.name ${USER_NAME}'
                sh 'git config --global user.email ${USER_EMAIL}'
                sh 'cat ~/.ssh/id_rsa'
                sh 'ls -all  / && ls /var/jenkins_home/workspace/'
                sh 'pwd && ls -all && ls /home'
                sh 'git config user.name'
                sh 'rm -rf  ./PackShellDemo/'
                sh 'git clone git@dev-gitlab.getui.net:lijm/PackShellDemo.git'
                sh 'echo checkout code ABCDEFG'
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