pipeline {

    agent any

    environment {

        AWS_REGION = "us-east-1"

        ACCOUNT_ID = "663130434850"

        FRONTEND_REPO = "${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/frontend"

        AUTH_REPO = "${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/auth-service"

        ADMIN_REPO = "${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/admin-service"

        CHAT_REPO = "${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/chat-service"

        STREAMING_REPO = "${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/streaming-service"

        IMAGE_TAG = "${BUILD_NUMBER}"

    }

    stages {

        stage('Checkout') {

            steps {

                git branch: 'main',
                url: 'https://github.com/suhailm67-sys/StreamingApp_Orchestration-and-Scaling.git'

            }

        }

        stage('Login to ECR') {

            steps {

                sh '''
                aws ecr get-login-password --region $AWS_REGION \
                | docker login \
                --username AWS \
                --password-stdin \
                $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
                '''

            }

        }

        stage('Build Frontend') {

            steps {

                sh '''
                docker build \
                -t $FRONTEND_REPO:$IMAGE_TAG \
                ./frontend
                '''

            }

        }

        stage('Build Auth Service') {

            steps {

                sh '''
                docker build \
                -t $AUTH_REPO:$IMAGE_TAG \
                ./backend/authService
                '''

            }

        }

        stage('Build Admin Service') {

            steps {

                sh '''
                docker build \
                -t $ADMIN_REPO:$IMAGE_TAG \
                -f backend/adminService/Dockerfile \
                backend
                '''

            }

        }

        stage('Build Chat Service') {

            steps {

                sh '''
                docker build \
                -t $CHAT_REPO:$IMAGE_TAG \
                -f backend/chatService/Dockerfile \
                backend
                '''

            }

        }

        stage('Build Streaming Service') {

            steps {

                sh '''
                docker build \
                -t $STREAMING_REPO:$IMAGE_TAG \
                -f backend/streamingService/Dockerfile \
                backend
                '''

            }

        }

        stage('Push Images') {

            steps {

                sh '''

                docker push $FRONTEND_REPO:$IMAGE_TAG

                docker push $AUTH_REPO:$IMAGE_TAG

                docker push $ADMIN_REPO:$IMAGE_TAG

                docker push $CHAT_REPO:$IMAGE_TAG

                docker push $STREAMING_REPO:$IMAGE_TAG

                '''

            }

        }

    }

}
