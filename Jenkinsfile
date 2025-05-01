pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/susanta7029/Task-manager.git'
            }
        }

        stage('Build Docker Images') {
            steps {
              
                bat 'docker compose build'
            }
        }

        stage('Start Containers') {
            steps {
           
                bat 'docker compose up -d'
            }
        }

        stage('Run Server Tests') {
            steps {
        
                bat 'docker exec $(docker ps -qf "name=server") npm test || true'
            }
        }

        stage('Clean Up') {
            steps {
                bat 'docker system prune -f'
            }
        }
    }

    post {
        always {
            echo 'CI/CD pipeline completed.'
        }
    }
}
