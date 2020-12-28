pipeline {
    agent {
        docker {
            image 'node:14-alpine'
            args '-p 23000:3000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the website? (Click "Process" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
