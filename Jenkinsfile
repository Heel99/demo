pipeline {
    agent any
      tools {
        nodejs 'nodejs 14' 
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
                
                    sh "aws s3 cp dist/ s3://bucketmul/dist/ "
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
