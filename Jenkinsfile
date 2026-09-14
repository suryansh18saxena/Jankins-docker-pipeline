pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        CONTAINER_NAME = "myapp-container"
        DOCKER = "docker"
    }

    stages {

        stage('Stop Existing Container') {
            steps {
                sh '''
                $DOCKER stop "$CONTAINER_NAME" 2>/dev/null || true
                $DOCKER rm "$CONTAINER_NAME" 2>/dev/null || true
                $DOCKER rmi "$IMAGE_NAME:latest" 2>/dev/null || true
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                $DOCKER build -t "$IMAGE_NAME:latest" .
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                $DOCKER run -d \
                --name "$CONTAINER_NAME" \
                -p 8080:80 \
                "$IMAGE_NAME:latest"
                '''
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
