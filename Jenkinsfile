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
                git branch: 'master', 
                url: 'https://github.com/ume950/MLOPS.git'
            }
        }
        stage('Test') {
            steps {
                script {
                    // sh 'pip install flake8'
                    // sh 'flake8 .'
                    // sh 'black --check .'
                    // Run unit tests for the backend
                    dir('/home/umesh/Downloads/MLOPS/mlops/src') {
                        sh 'python3 -m unittest discover tests'
                    }
                }
            }
        }
        // stage('Build Docker Images') {
        //     steps {
        //         script {
        //             // Build Docker images
        //             sh 'docker build -t adityavit36/carprice -f /home/aditya/adityamin/MLOPS/mlops/src/react_docker /home/aditya/adityamin/MLOPS/mlops'
        //             sh 'docker build -t adityavit36/predictor-app -f /home/aditya/adityamin/MLOPS/mlops/src/predictor-app /home/aditya/adityamin/MLOPS/mlops/src'
        //             sh 'docker build -t adityavit36/model-loader -f /home/aditya/adityamin/MLOPS/mlops/src/model_loader_dockerfile /home/aditya/adityamin/MLOPS/mlops/src'
        //         }
        //     }
        // }
        // stage('Push Docker Images') {
        //     steps {
        //         script {
        //             docker.withRegistry('', 'DockerHubCred') {
        //                 sh 'docker push adityavit36/carprice:latest'
        //                 sh 'docker push adityavit36/predictor-app:latest'
        //                 sh 'docker push adityavit36/model-loader:latest'
        //             }
        //         }
        //     }
        // }
        // stage('Run Ansible Playbook') {
        //     steps {
        //         ansiblePlaybook(
        //             playbook: 'deploy.yml',
        //             inventory: 'inventory'
        //         )
        //     }
        //}
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
