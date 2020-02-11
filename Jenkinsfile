pipeline {
	
	agent any 
	
	stages {
	
		stage("Building an artifact") [
			steps {
				echo "Building an artifact"
				sh label: '', script: 'mvn clean package'
				echo "Archieving an artifact"
				archiveArtifacts '**/*.jar'
			}
		}
		
		stage("Buiding Docker image") {
			steps {
			    echo "Buiding an image"
				sh label: '', script: 'docker build -t kiranfegade121/hello-world-rest-api:3.0 .'
			}
		}
		
		stage("Publish an image to Docker hub") {
			withCredentials([usernamePassword(credentialsId: 'DOCKER_HUB_CREDENTIALS', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
				echo "Logging into Docker hub"
				sh label: '', script: 'docker login -u $USERNAME -p $PASSWORD'
				echo "Pushing an image to Docker hub"
				sh label: '', script: 'docker push kiranfegade121/hello-world-rest-api:3.0'
			}		
		}
	}
}