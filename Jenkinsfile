pipeline {
    agent any

    environment {
        SONARQUBE = 'MySonar' // Убедись, что настроено в Jenkins → Configure System
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/vladtheloka/weather-app.git' // или локальный путь
            }
        }

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
