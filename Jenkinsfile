pipeline {
    agent any
    environment {
        DOCKER_HUB_USERNAME = 'umeshjaware'
        CARPRICE_IMAGE_NAME = 'carprice'
        PREDICTOR_IMAGE_NAME = 'predictor-app'
        MODEL_LOADER_IMAGE_NAME = 'model-loader'
	// EC2_INSTANCE_IP = '65.0.248.48'
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                git branch: 'main', 
                url: 'https://github.com/ume950/MLOPS.git'
            }
        }
       stage('Test') {
    steps {
        script {
            // Install the specific versions of the required Python packages
            sh 'pip install flask==3.0.3 numpy==1.26.4 flask_cors==4.0.0 scikit-learn==1.3.0'

            // Change the working directory to where your tests are located
            dir('/home/umesh/Downloads/MLOPS/mlops/src') {
                // Run unit tests for the backend and redirect output to a log file
                sh 'python3 -m unittest discover -s . -p "test_app.py" > test_results.log 2>&1'
            }
        }
    }
}



        stage('Build Docker Images') {
            steps {
                script {
                    // Build Docker images
                    sh 'docker build -t umeshjaware/carprice -f /home/umesh/Downloads/MLOPS/mlops/src/react_docker /home/umesh/Downloads/MLOPS/mlops/'
                    sh 'docker build -t umeshjaware/predictor-app -f /home/umesh/Downloads/MLOPS/mlops/src/predictor-app /home/umesh/Downloads/MLOPS/mlops/src/'
                    sh 'docker build -t umeshjaware/model-loader -f /home/umesh/Downloads/MLOPS/mlops/src/model_loader_dockerfile /home/umesh/Downloads/MLOPS/mlops/src/'
                }
            }
        }
        stage('Push Docker Images') {
            steps {
                script {
                    docker.withRegistry('', 'DockerHubCred') {
                        sh 'docker push umeshjaware/carprice:latest'
                        sh 'docker push umeshjaware/predictor-app:latest'
                        sh 'docker push umeshjaware/model-loader:latest'
                    }
                }
            }
        }
        // stage('Run Ansible Playbook') {
        //     steps {
        //         ansiblePlaybook(
        //             playbook: 'deploy.yml',
        //             inventory: 'inventory'
        //         )
        //     }
        // }
   //      stage('Deploy to EC2') {
	  //       steps {
	  //           ansiblePlaybook(
	  //               playbook: 'deploy-ec2.yml',
	  //               inventory: 'ec2-inventory',
			// credentialsId: '41668044-b19d-41a2-98ac-6d281b0a30d9',
			// extras: '-e ansible_user=ec2-user -e ansible_ssh_private_key_file=/home/aditya/Downloads/adityavit36_spe.pem'
	  //           )
   //  	    }
    	// }
    }
}
