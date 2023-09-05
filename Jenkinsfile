pipeline {
    agent any
    
    environment {
        AWS_ACCESS_KEY_ID =('AKIAYBNQXIQPISFMBGGH')
        AWS_SECRET_ACCESS_KEY = ('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') 
        S3_BUCKET_NAME = 'bucketmul' 
    }

    stages {
       
        stage('Build Project') {
            steps {
                
                sh "npm i @angular/cli@13.2.1 && npm run build" 
            }
        }

        stage('Upload to S3') {
            steps {
                script {
                
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
