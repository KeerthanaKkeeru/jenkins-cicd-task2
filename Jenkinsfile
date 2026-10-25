
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Getting source code from GitHub'
                checkout scm
            }
        }

        stage('Test') {
            steps {
                echo 'Testing JavaScript syntax'
                bat 'npm test'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Docker image'
                bat 'docker build -t jenkins-cicd-task2 .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'

                bat '''
                docker rm -f jenkins-task2-app 2>NUL
                docker run -d --name jenkins-task2-app -p 3000:3000 jenkins-cicd-task2
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
