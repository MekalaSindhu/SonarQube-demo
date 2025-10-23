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
                    sh '''
                    sonar-scanner \
                      -Dsonar.projectKey=SonarQube-demo \
                      -Dsonar.sources=. \
                      -Dsonar.host.url=http://192.168.0.115:9000 \
                      -Dsonar.login=$SONAR_AUTH_TOKEN
                    '''
                }
            }
        }

        stage('Quality Gate') {
            steps {
                tim
