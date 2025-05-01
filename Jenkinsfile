pipeline {
    agent {
        kubernetes {
            label 'jenkins-agent'
            defaultContainer 'jnlp'
        }
    }
 tools {
        git 'Default'  
        dockerTool 'docker'
    }
 environment {
        REPORT_NAME = 'trivy-report.html'
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
        stage('Trivy Scan') {
            steps {
                echo 'Running Trivy to scan the repo...'
                sh '''
                    docker run --rm -v $(pwd):/repo aquasec/trivy fs --format template --template "@contrib/html.tpl" -o ${REPORT_NAME} /repo
                '''
            }
        }

        stage('Publish Trivy Report') {
            steps {
                publishHTML(target: [
                    reportDir: '.', 
                    reportFiles: "${REPORT_NAME}", 
                    reportName: 'Trivy Scan Report'
                ])
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: "${REPORT_NAME}", fingerprint: true
        }
    }

        
}

