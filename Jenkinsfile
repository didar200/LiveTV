pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
              script {
                kubernetesDeploy (configs: 'webserver.yaml',kubeconfigId: 'kubernetes')
              }
            }
        }
    }
}
