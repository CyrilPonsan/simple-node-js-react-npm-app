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

        stage('Install Dependencies') {
            steps {
                echo "Hello Toto"
                // Install npm dependencies
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                withCredentials([string(credentialsId: 'SECRET_MESSAGE', variable: 'MY_SECRET_TEXT')]) {
                    echo MY_SECRET_TEXT
                    // Build the application (if required)
                    sh 'npm run build'
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
