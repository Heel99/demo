pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        AWS_ACCESS_KEY_ID = credentials('AKIA5IHLUIJ3PW3WKOQZ')
        AWS_SECRET_ACCESS_KEY = credentials('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')
        S3_BUCKET_NAME = 'angularbucket12'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'npm install'
                    sh 'ng build --prod'
                }
            }
        }

        stage('Upload to S3') {
            steps {
                script {
                    def awsS3 = [:]
                    awsS3['AWS_REGION'] = AWS_DEFAULT_REGION
                    awsS3['AWS_ACCESS_KEY_ID'] = AWS_ACCESS_KEY_ID
                    awsS3['AWS_SECRET_ACCESS_KEY'] = AWS_SECRET_ACCESS_KEY

                    withAWS(credentials: awsS3, region: awsS3['AWS_REGION']) {
                        sh "aws s3 sync dist/ s3://${S3_BUCKET_NAME}/"
                    }
                }
            }
        }
    }

    post {
        always {
          node{
            cleanWs()
           }
        }
    }
}
