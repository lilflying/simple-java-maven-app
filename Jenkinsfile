pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'echo "Build en cours..."'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Tests en cours..."'
            }
        }
        stage('Deploy') {
            steps {
                writeFile file: 'Dockerfile', text: '''
FROM eclipse-temurin:11-jre
WORKDIR /app
COPY . .
CMD ["echo", "App deployed (demo)"]
'''
                sh 'docker build -t mon-app:latest .'
                sh '''
                  docker rm -f mon-app || true
                  docker run -d --name mon-app --network devops mon-app:latest
                '''
            }
        }
    }
}
