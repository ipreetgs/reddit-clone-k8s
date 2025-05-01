pipeline {
    agent {
        kubernetes {
            label 'jenkins-agent'
            defaultContainer 'jnlp'
        }
    }
    stages {
        stage('Test') {
            steps {
                container('jnlp') {
                    sh 'echo "Hello from a dynamic Kubernetes pod!"'
                }
            }
        }
    }
}
