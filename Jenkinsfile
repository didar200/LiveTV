pipeline {
    agent any
	
    environment {
        dockerImage =''
        registry = 'didar200/livewebserver'
        redistryCredential = 'dockerhub'
    }

    stages {
        stage('Build docker image'){
            steps{
                script{
                    dockerImage = docker.build registry
                }
            }
        }

	stage('Push') {
            steps {
                script{
                    docker.withRegistry( '', registryCredential ) {
			dockerImage.push()
		    }
                }
	    }
	}
        stage('Deploy to K8s') {
            steps {
              script {
                kubernetesDeploy (configs: 'webserver.yaml',kubeconfigId: 'kubernetes')
              }
            }
        }
    }
}
