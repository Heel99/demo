pipeline {
    agent any
   tools {
        nodejs 'nodejs'
    }

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
              sh 'aws s3 cp dist/* s3://bucketmul/ --recursive'
              }
          }
    }
}
