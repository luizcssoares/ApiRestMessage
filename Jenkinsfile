pipeline {
      agent any
      environment {
	 registry = 'var/lib/jenkins/workspace/ApiRestMessage/target/ApiRestMessage-0.0.1-SNAPSHOT.jar'     
         dockerhub_credentials = 'luizcssoares-dockerhub'
	 docker_image = ''     
      }	 
      stages {		    
	      stage('GIT pull') {
		      steps{  
			   dir('ApiRestMensagem') {   
		               git url: "https://github.com/luizcssoares/ApiRestMessage.git"
			   }				   
		      }
	      }
	      stage('Build Maven') {		
		      steps {
		           sh 'mvn -B -DskipTests clean package'     
		      }
	      }	
	      stage('Docker Build'){
		      steps {		
			   sh 'docker build -t var/lib/jenkins/workspace/ApiRestMessage/target/ApiRestMessage-0.0.1-SNAPSHOT.jar'   			   
		      }
	      }	  	      	      
	      stage('Deploy our image') {
		      steps{  
			      script {
				 echo "pushing " + docker_image
				      docker.withRegistry( '', dockerhub_creentials ) {
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
