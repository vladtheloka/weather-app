pipeline {
    agent {
        docker {
            image 'python:3.10-slim'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        SONARQUBE = 'MySonar'
    }

    stages {
        stage('Install deps & test') {
            steps {
                sh 'pip install -r requirements.txt'
                sh 'pytest tests/'
            }
        }

        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv(SONARQUBE) {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t weather-app .'
            }
        }
    }
}

