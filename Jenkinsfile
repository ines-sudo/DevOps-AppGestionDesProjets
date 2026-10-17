pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verification Docker') {
            steps {
                sh 'docker --version'
                sh 'docker compose version'
            }
        }

        stage('Build Backend') {
            steps {
                sh 'docker build -t gestion-backend:latest ./backend'
            }
        }

        stage('Build Frontend') {
            steps {
                sh 'docker build -t gestion-frontend:latest ./frontend'
            }
        }

        stage('Verification Images') {
            steps {
                sh 'docker image inspect gestion-backend:latest'
                sh 'docker image inspect gestion-frontend:latest'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploiement de l application...'
                sh 'docker compose up -d --build'
                sh 'docker compose ps'
            }
        }
    }

    post {
        success {
            echo 'Pipeline Jenkins termine avec succes !'
        }

        failure {
            echo 'Erreur pendant le pipeline Jenkins.'
        }
    }
}
