pipeline {
    agent any
	
	environment{
		DOCKERHUB_SECRETS=credentials('jenkins')
		IMAGE_NAME="gwakbyeongguk/jenkin_nodejs"
		IMAGE_TAG="latest"	
	}
	
    stages {
        stage('clone from SCM') {
            steps {
                git url: 'https://github.com/GwakByeongGuk/jenkins_fastapi.git', branch: 'main'
            }
        }
		
		stage('Docker build and desplay'){
			steps {
				sh '''
				docker compose build
				'''
			}
		}
		
		stage('Logging into Docker Hub'){
			steps {
				sh '''
				echo ${DOCKERHUB_SECRETS_PSW} | docker login -u ${DOCKERHUB_SECRETS_USR} --password-stdin
				'''
			}
		}
		
		stage('Pushing Docker image to Docker Hub'){
			steps {
				sh '''
				docker tag siestageek/nodejs-app ${IMAGE_NAME}:${IMAGE_TAG}
				docker push ${IMAGE_NAME}:${IMAGE_TAG}
				'''
			}
		}
		stage('Docker Hub logout'){
			steps {
				sh '''
				docker logout
				'''
			}
		}
    }
}
