pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker-compose build
                docker-compose push 
                '''
            }
        }
        stage('Deploy') [
            steps {
                sh '''
                ssh -i "~/.ssh/id_rsa" jenkins@34.175.144.0 << EOF
                rm -rf LBG-Python-API
                git clone https://github.com/stevenpwilson/LBG7-Python-API.git
                cd LBG-Python-API
                docker-compose down
                docker-compose up -d
                '''
            }
        ]
        stage('Clean up') {
            steps {
                sh '''
                docker system prune --force
                ssh -i "~/.ssh/id_rsa" jenkins@34.175.144.0 << EOF 
                docker system prune --force
                '''
            }
        }
    }
}
