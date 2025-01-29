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

        stage('Verify Build Output') {
            steps {
                script {
                    sh '''
                    echo "Listing files in dist/"
                    ls -alh dist/
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['linux-host']) {
                    script {
                        sh '''
                        ssh -o StrictHostKeyChecking=no root@10.168.10.141 <<EOF
                        echo "Deploying the Angular app"
                        # Clear the existing build files in the target directory
                        rm -rf /var/www/html/*
                        # Copy new build files from Jenkins workspace to the remote server
                        cp -r /var/jenkins_home/workspace/jenkins_web/dist/* /var/www/html/
                        EOF
                        '''
                    }
                }
            }
        }
    }
}
