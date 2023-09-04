pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                sh 'npm install'
                sh 'npm run build'
                sh 'npm test'
            }
        }

        stage('Publish to S3') {
            steps {
                s3Upload(entries: 'dist/*', bucket: 'bucketmul', doNotArchiveArtifacts: false)
            }
        }
    }
}
