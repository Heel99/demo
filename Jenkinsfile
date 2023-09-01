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
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Deploy to S3') {
            steps {
                withAWS(credentials: 'your-aws-credentials-id', region: 'us-east-1') {
                    sh 'aws s3 sync dist/ s3://your-s3-bucket-name'
                }
            }
        }
    }
}
