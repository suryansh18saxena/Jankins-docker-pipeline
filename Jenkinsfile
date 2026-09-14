pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        CONTAINER_NAME = "myapp-container"
        PODMAN = "podman --cgroup-manager=cgroupfs"
    }

    stages {

        stage('Stop Existing Container') {
            steps {
                sh '''
                $PODMAN stop "$CONTAINER_NAME" 2>/dev/null || true
                $PODMAN rm "$CONTAINER_NAME" 2>/dev/null || true
                $PODMAN rmi "$IMAGE_NAME:latest" 2>/dev/null || true
                '''
            }
        }

        stage('Build Podman Image') {
            steps {
                sh '''
                $PODMAN build -t "$IMAGE_NAME:latest" .
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                $PODMAN run -d \
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
