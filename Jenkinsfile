pipeline {
    agent any

    stages {
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t didar200/livewebserver .'
                }
            }
        }
        
	stage('Login') {
	    steps {
                script {
		    sh 'echo $dockerhubpwd | docker login -u $dockerhubusr --password-stdin'
                }
	    }
	}

	stage('Push') {
            steps {
                script{
                    sh 'docker push didar200/livewebserver'
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
