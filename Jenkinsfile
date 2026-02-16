pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devsecops-demo .'
            }
        }

        stage('Security Scan') {
            steps {
                sh 'trivy image devsecops-demo'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker stop devsecops-container || true'
                sh 'docker rm devsecops-container || true'
                sh 'docker run -d -p 5000:5000 --name devsecops-container devsecops-demo'
            }
        }
    }
}
