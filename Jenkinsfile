pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                git branch: 'main', url: 'https://github.com/Murali-Kaspa/My-Portifolio.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Add build steps here if needed (e.g., compiling code)
                    echo 'Build step: Skippd for now.'
                }
            }
        }
        stage('Test') {
            steps {
                // Run tests (if applicable)
                echo 'Running tests..'
                // Example: sh './run-tests.sh'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Deploy the application to the target server
                    sshagent(['MacbookKeypair.pem']) {
                        sh '''
                        ssh -i Macbook_Keypair.pem ec2-user@3.108.52.220 <<EOF
                        cd /path/to/deployment/directory
                        git pull origin main
                        nohup python3 app.py &
                        EOF
                        '''
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
