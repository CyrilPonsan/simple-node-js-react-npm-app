pipeline {
    agent {
        docker {
            image 'node:20'
            args '-u root' // Run the container as root to avoid permission issues
        }
    }


    environment {
        NODE_VERSION = '20.x'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                git 'https://github.com/CyrilPonsan/simple-node-js-react-npm-app.git'
            }
        }

        stage('Setup Node.js') {
            steps {
                // Set up Node.js environment
                sh '''
                    curl -sL https://deb.nodesource.com/setup_$NODE_VERSION | bash -
                    apt-get install -y nodejs
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install npm dependencies
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                // Build the application (if required)
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['secret_ssh']) {
                    sh '''
                        scp -r * admin@ec2-13-39-155-135.eu-west-3.compute.amazonaws.com
                    '''
                }
            }
        }
    }

    post {
        always {
            // Cleanup, notifications, etc.
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
