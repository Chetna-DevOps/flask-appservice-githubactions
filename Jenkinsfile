pipeline {
    agent any
    stages {
        stage('Pull Code on VM') {
            steps {
                sshagent(['azure-vm-ssh']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no azureuser@20.244.108.70 "
                            cd /app &&
                            git pull origin main
                        "
                    '''
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sshagent(['azure-vm-ssh']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no azureuser@20.244.108.70 "
                            cd /app &&
                            source venv/bin/activate &&
                            pip install -r requirements.txt
                        "
                    '''
                }
            }
        }
        stage('Run Migrations') {
            steps {
                sshagent(['azure-vm-ssh']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no azureuser@20.244.108.70 "
                            cd /app &&
                            source venv/bin/activate &&
                            flask db upgrade
                        "
                    '''
                }
            }
        }
        stage('Restart App') {
            steps {
                sshagent(['azure-vm-ssh']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no azureuser@20.244.108.70 "
                            sudo systemctl restart flaskapp
                        "
                    '''
                }
            }
        }
    }
    post {
        success {
            echo 'Flask app deployed successfully!'
        }
        failure {
            echo 'Deployment failed. Check logs above.'
        }
    }
}
