pipeline {
    agent any

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
                withCredentials([string(credentialsId: 'my_secret_text_id', variable: 'MY_SECRET_TEXT')]) {
                    echo MY_SECRET_TEXT
                    // Build the application (if required)
                    sh 'npm run build'
                }
            }
        }
    }
}