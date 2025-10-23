pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/MekalaSindhu/SonarQube-demo.git'
            }
        }

        stage('SonarQube Analysis') {
            environment {
                SONAR_AUTH_TOKEN = credentials('SONAR_AUTH_TOKEN')
            }
            steps {
                withSonarQubeEnv('SonarQube') {
                    tool 'SonarScanner'
                    sh 'sonar-scanner -Dsonar.projectKey=SonarQube-demo -Dsonar.sources=.'
                }
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
