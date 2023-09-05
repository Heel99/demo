pipeline {
    agent any
    
    environment {
        AWS_ACCESS_KEY_ID = credentials('AKIAYBNQXIQPISFMBGGH')
        AWS_SECRET_ACCESS_KEY = credentials('67Z5uTTZ19vwvN6o+27qHhYP9D9elHUsi+76DgNh') 
        S3_BUCKET_NAME = 'bucketmul' 
        PROJECT_DIR = '/demo' // Replace with the actual path to your project
        DIST_DIR = 'dist' // Replace with the directory containing your distribution files
    }

    stages {
        stage('Checkout') {
            steps {
                git clone https://github.com/Heel99/demo
                  
            }
        }

        stage('Build Project') {
            steps {
                // Build your project distribution
                sh "cd ${PROJECT_DIR} && npm i @angular/cli@13.2.1 && npm run build" 
            }
        }

        stage('Upload to S3') {
            steps {
                script {
                    sh 'curl "https://d1vvhvl2y92vvt.cloudfront.net/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"'
                    sh 'unzip awscliv2.zip'
                    sh './aws/install'

                    
                    sh "aws s3 cp ${PROJECT_DIR}/${DIST_DIR} s3://${S3_BUCKET_NAME}/${DIST_DIR} --recursive"
                }
            }
        }
    }

    post {
        success {
            echo 'Build and upload to S3 succeeded.'
        }
        failure {
            echo 'Build or upload to S3 failed.'
        }
    }
}
