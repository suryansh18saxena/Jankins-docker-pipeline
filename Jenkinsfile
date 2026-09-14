pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        CONTAINER_NAME = "myapp-container"
    }

    stages {

        stage('Stop Existing Container') {
            steps {
                sh '''
                podman stop myapp-container || true
                podman rm myapp-container || true
                podman rmi myapp:latest || true
                '''
            }
        }

        stage('Build Podman Image') {
            steps {
                sh '''
                podman build -t myapp:latest .
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                podman run -d \
                --name myapp-container \
                -p 8080:80 \
                myapp:latest
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
