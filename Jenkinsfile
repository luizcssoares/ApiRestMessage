pipeline {
      agent any
      environment {
	 registry = 'luizcssoares/apirestmessage'
         dockerhub_credentials = 'luizcssoares-dockerhub'
	 docker_image = ''     
      }	 
      stages {		    
	      stage('GIT pull') {
		      steps{  
			    git url: "https://github.com/luizcssoares/ApiRestMessage.git"
		      }				   		      
	      }
	      stage('Build Maven') {		
		      steps {
		           sh 'mvn -B -DskipTests clean package'     
		      }
	      }	
	      stage('Docker Build'){
		      steps{
			   script {		
				   docker_image = docker.build  registry
			    }
		      }
	      }	  	      	      
	      stage('Deploy our image') {
		      steps{  
			      script {
				 echo "pushing " + docker_image
				      docker.withRegistry( '', dockerhub_credentials ) {
					 docker_image.push()
				      }
				 echo "pushed"
			      }
		      }
	      }	      
	      stage('Kubernetes'){
		      steps {
		           sh 'kubectl apply -f deployment.yml'
		      }
	      }	        
      }  
}
