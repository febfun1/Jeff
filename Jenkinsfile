
pipeline{

   agent any

	//create dockerhub credential in github with your dockerhub Username and Password/Token
	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}
	
	stages {

		stage('gitclone') {

		      steps {
		         git 'https://github.com/adeoyedewale/Jeff.git'
		      }
		}
		
		stage('Build') {
			steps {
			
			   sh 'docker build -t eruobodo/class_app:${BUILD_NUMBER} .'
			}
		}
		
		stage('Login') {
		
			steps {
			   sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login --username eruobodo --password-stdin'    
			}
		}

		stage('Push') {
			
			steps {
			   sh 'docker push eruobodo/class_app:${BUILD_NUMBER}'
			}
		}
		}
	
	post {
	    always {
		sh 'docker logout'
	    }
    }

}
