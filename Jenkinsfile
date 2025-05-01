pipeline {
    agent {
        kubernetes {
            label 'jenkins-agent'
            defaultContainer 'jnlp'
        }
    }
 tools {
        git 'Default'  
    }
    stages {
        stage('Test Pod') {
            steps {
                container('jnlp') {
                    sh 'echo "Hello from a dynamic Kubernetes pod!"'
                }
            }
            }
        stage('Clone Codebase') {
            steps {
                container('jnlp') {
                    git branch: 'main',
                        url: 'https://github.com/ipreetgs/reddit-clone-k8s.git'
                }
            }
        }
        
        }
}

