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
		
		stage("build an image") {
			steps {
				echo "creating an image..."
				bat label: '', script: 'docker build -t kiranfegade121/hello-world-rest-api:3.0 .'
			}			
		}
		
		stage("push docker image") {
			steps {
				echo "pushing and image to docker hun"
				bat label: '', script: 'docker push kiranfegade121/hello-world-rest-api:3.0'
			}
		}
		
		stage("deploy on kubernetes cluster") {
			steps {
				kubernetesDeploy configs: 'deployment.yml', kubeConfig: [path: ''], kubeconfigId: 'kubeconfig', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']	
			}
		}
		
		
	}
}			
