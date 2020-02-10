pipeline {
	
	agent any 
	
	
	stages {
	
		stage("build and archieve an artifact") {
			steps {
				echo "Building an artifact..."
				sh label: '', script: 'mvn clean package'
				echo "Archiving an artifact..."
				archiveArtifacts '**/*.jar'
			}
		}
		
		stage("build and push an image") {
			steps {
				echo "creating an image..."
				script {					
					withDockerRegistry(credentialsId: 'docker-hub-cred', url: 'http://registry.hub.docker.com') {
						app = docker.build("kiranfegade121/hello-world-rest-api:3.0");
						app.push()
					}
					
				}
			}			
		}	
		
	}
}			
