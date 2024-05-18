pipeline {
    agent any

    environment {
        // Define the Docker image names
        CARPRICE_IMAGE_NAME = 'carprice'
        PREDICTOR_IMAGE_NAME = 'predictor-app'
        MODEL_LOADER_IMAGE_NAME = 'model-loader'
        DOCKER_HUB_USERNAME = 'umeshjaware'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                git branch: 'main', 
                url: 'https://github.com/ume950/MLOPS.git'
            }
        }

        stage('Pull Docker Images') {
            steps {
                script {
                    // Pull Docker images from Docker Hub
                    docker.image("${DOCKER_HUB_USERNAME}/${CARPRICE_IMAGE_NAME}:latest").pull()
                    docker.image("${DOCKER_HUB_USERNAME}/${PREDICTOR_IMAGE_NAME}:latest").pull()
                    docker.image("${DOCKER_HUB_USERNAME}/${MODEL_LOADER_IMAGE_NAME}:latest").pull()
                }
            }
        }

        stage('Run Docker Compose') {
            steps {
                script {
                    // Run Docker Compose in the specified directory
                    dir('/home/umesh/Downloads/MLOPS/mlops/src') {
                        sh 'docker compose up -d'
                    }
                }
            }
        }

        stage('Send Logs to Logstash') {
            steps {
                logstashSend build: env.BUILD_NUMBER, maxLines: 10000, maxRetries: 5
            }
        }
    }
}
