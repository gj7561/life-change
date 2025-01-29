pipeline {
    agent any

    environment {
        NODE_VERSION = '18'
    }

    stages {
        stage('Install Node.js with nvm') {
            steps {
                script {
                    sh '''
                    export NVM_DIR="$HOME/.nvm"
                    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                    nvm install $NODE_VERSION
                    nvm use $NODE_VERSION
                    node -v
                    npm install
                    '''
                }
            }
        }

        stage('Build Angular App') {
            steps {
                script {
                    sh '''
                    export NVM_DIR="$HOME/.nvm"
                    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                    npm run build --prod
                    '''
                }
            }
        }
    }
}
