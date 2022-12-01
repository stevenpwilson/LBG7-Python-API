pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                /usr/local/bin/docker-compose build
                /usr/local/bin/docker-compose push 
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                docker-compose down
                docker-compose up -d
                '''
            }
        }
        stage('Clean up') {
            steps {
                sh '''
                docker system prune --force
                '''
            }
        }
    }
}
