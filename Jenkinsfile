pipeline {
	
	agent any
	
	stages {
	
		stage("Build an artifact") {
			steps {
				echo "Building an artifact"
				sh label: '', script: 'mvn clean package'
				echo "Archiving an artifact"
				archiveArtifacts '**/*.jar'
			}			
		}
		
		stage("Building an image") {
		    steps {
				sh label: '', script: 'docker build -t kiranfegade121/hello-world-rest-api:3.0 .'
			}			
		}		
		
		stage("Push an image to docker hub") {
		    steps {
				withCredentials([usernamePassword(credentialsId: 'docker-hub-dredentials', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
					sh label: '', script: 'docker login -u $USERNAME -p $PASSWORD'
					sh label: '', script: 'docker push kiranfegade121/hello-world-rest-api:3.0'
				}
			}				
		}
	}
}