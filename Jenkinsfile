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
                sh 'export GIT_SSL_NO_VERIFY=1&&git config --global http.sslverify false'
                sh 'git config --global user.name lijm'
                sh 'git config --global user.password l10101125'
                sh 'ls /var/'
                sh 'ls -all  / && ls /var/jenkins_home/workspace/'
                sh 'pwd && ls -all && ls /home'
                sh 'git config user.name'
                sh 'git clone https://lijm:l10101125@dev-gitlab.getui.net/lijm/PackShellDemo.git'
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