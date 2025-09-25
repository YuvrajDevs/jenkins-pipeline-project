pipeline{
	agent any
	tools{
		node 'NodeJS-LTS'
	}
	environment{
		DOCKERHUB_USERNAME = 'yuvrajdevs'
		IMAGE_NAME = "${DOCKERHUB_USERNAME}/jenkins-pipeline-project"
		IMAGE_TAG = "build-${BUILD_NUMBER}"
	}
	stages{
		stage('Build and Test'){
			steps{
				echo 'Installing Dependencies...'
				sh 'npm install'
				sh 'npm test'
			}
		}
		stage('Build Docker Image'){
			steps{
				echo 'Building docker image...'
				sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
			}
		}
		stage('Push Docker Image'){
			steps{
				withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]){
					sh "docker login -u ${DOCKER_USER} -p ${DOCKER_pass}"
					sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
				}
			}
		}
	}
}
