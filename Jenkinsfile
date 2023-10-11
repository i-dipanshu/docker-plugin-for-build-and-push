pipeline {
    agent any

    environment {
        // Define the Docker Hub credentials from Jenkins secret
        DOCKERHUB_CREDENTIAL = credentials('docker-cred')
        DOCKER_IMAGE_NAME = 'simple-django-app'
        REGISTRY_URL = 'https://registry.hub.docker.com'
    }

    stages {

        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile
                    def newImage = docker.build(env.DOCKER_IMAGE_NAME, "-f Dockerfile .")
                    // Authenticate with Docker Hub using the Jenkins secret credential

                    sh 'echo "Build Successfully"'

                    // docker.withRegistry(env.REGISTRY_URL, env.DOCKERHUB_CREDENTIAL) {
                    //     // Push the built image to Docker Hub
                    //     newImage.push("${env.BUILD_NUMBER}")
                    // }

                    docker.withRegistry(env.REGISTRY_URL, 'docker-id-passwd') {
                        // Push the built image to Docker Hub
                        newImage.push("${env.BUILD_NUMBER}")
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
