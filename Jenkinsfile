pipeline {
    agent {
        kubernetes {
            label 'jenkins-agent'
            defaultContainer 'jnlp'
        }
    }
 tools {
        git 'Default'         // The Git installation name configured in Jenkins
        dockerTool 'Docker'   // The Docker installation name configured in Jenkins
    }
    stages {
        stage('Clone Codebase') {
            steps {
                container('jnlp') {
                    git branch: 'main',
                        url: 'https://github.com/your-username/your-repo.git'
                }
            }
        }
        stage('Test') {
            steps {
                container('jnlp') {
                    sh 'echo "Hello from a dynamic Kubernetes pod!"'
                }
            }
        }
    }
}
