pipeline {
    agent any

    environment {
        // Define the Docker Hub credentials from Jenkins secret
        DOCKERHUB_CREDENTIAL = credentials('docker-cred')
        DOCKER_IMAGE_NAME = 'simple-flask-app'
    }

    stages {

        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile
                    def newImage = docker.build(env.DOCKER_IMAGE_NAME, "-f Dockerfile .")
                    // Authenticate with Docker Hub using the Jenkins secret credential
                    docker.withRegistry('', env.DOCKERHUB_CREDENTIAL) {
                        // Push the built image to Docker Hub
                        newmage.push("${env.BUILD_NUMBER}")
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image build and push successful'
        }

        failure {
            echo 'Docker image build or push failed'
        }
    }
}
