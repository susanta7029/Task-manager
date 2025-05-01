pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Sam123336/task-manager.git'
            }
        }

        stage('Build Docker Images') {
            steps {
              
                sh 'docker compose build'
            }
        }

        stage('Start Containers') {
            steps {
           
                sh 'docker compose up -d'
            }
        }

        stage('Run Server Tests') {
            steps {
        
                sh 'docker exec $(docker ps -qf "name=server") npm test || true'
            }
        }

        stage('Clean Up') {
            steps {
                sh 'docker system prune -f'
            }
        }
    }

    post {
        always {
            echo 'CI/CD pipeline completed.'
        }
    }
}
