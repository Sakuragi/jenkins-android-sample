pipeline{
    agent {
        docker {
            image 'allbears/jenkins-android:1.0.1'
        }
    }
    stages {
        stage('Build'){
             steps {
                sh './gradlew clean && rm -rf ./app/build/'
                sh './gradlew assembleRelease'
             }
        }
       stage('UnitTest'){
             steps {
                sh './gradlew test'
             }
        }

    }

}