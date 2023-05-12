pipeline {
      agent any
      environment {
         DOCKERHUB_CREDENTIALS = credentials('luizcssoares-dockerhub')
      }	 
      stages {	
	      stage('GIT push') {
		      steps{  
		           git url: "https://github.com/luizcssoares/ApiRestMessage.git"
		      }
	      }
	      stage('Build Maven') {		
		      steps {
		           bat 'mvn clean package'     
		      }
	      }	
	      stage('Docker Build'){
		      steps {
		           bat 'docker build -t luizcssoares/apirestmessage .'
		      }
	      }	    
	      stage('Push DockerHub'){
		      steps {
		           bat 'docker push luizcssoares/apirestmessage'
		      }
	      }	
	      stage('Kubernetes'){
		      steps {
		           bat 'kubectl apply -f deployment.yml'
		      }
	      }	        
      }  
}
