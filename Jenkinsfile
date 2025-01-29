pipeline {
    agent any

    environment {
        NODE_VERSION = '18'  // Set Node.js version (adjust as needed)
        BUILD_DIR = 'dist/*'  // Adjust based on Angular project name
        DEPLOY_SERVER = 'user@your-server.com' // Change to your deployment server
        DEPLOY_PATH = '/var/www/html/' // Change to your desired path
    }

    stages {
        

        stage('Install Node.js') {
            steps {
                script {
                    sh "nvm install $NODE_VERSION || true"
                    sh "nvm use $NODE_VERSION || true"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Angular App') {
            steps {
                sh 'npm run build '
            }
        }

        stage('Deploy to Server') {
            steps {
                script {
                    sh "scp -r $BUILD_DIR/* $DEPLOY_SERVER:$DEPLOY_PATH"
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build & Deployment Successful!'
        }
        failure {
            echo '❌ Build or Deployment Failed!'
        }
    }
}
