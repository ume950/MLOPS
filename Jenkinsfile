pipeline {
    agent any

    environment {
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
                    // Pull carprice Docker image from Docker Hub
                    docker.image("${DOCKER_HUB_USERNAME}/${CARPRICE_IMAGE_NAME}:latest").pull()

                    // Pull predictor-app Docker image from Docker Hub
                    docker.image("${DOCKER_HUB_USERNAME}/${PREDICTOR_IMAGE_NAME}:latest").pull()

                    // Pull model-loader Docker image from Docker Hub
                    docker.image("${DOCKER_HUB_USERNAME}/${MODEL_LOADER_IMAGE_NAME}:latest").pull()
                }
            }
        }

        stage('Run Docker Compose') {
            steps {
                script {
                    dir('/home/umesh/Downloads/speproject-master') {
                        sh 'docker compose up -d'
                    }
                }
            }
        }
    }
}
