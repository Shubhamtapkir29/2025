pipeline {
    agent {
       label "shubham-node"
    }

    environment {
        DEPLOY_DIR = "/var/www/html"
        BRANCH = "2025Q1"
        REPO = "https://github.com/Shubhamtapkir29/2025.git"
    }

    stages {
        stage('Clean Deploy Directory') {
            steps {
                script {
                    sh "sudo rm -rf ${DEPLOY_DIR}/*"
                }
            }
        }

        stage('Clone Repo') {
            steps {
                git branch: "${BRANCH}", url: "${REPO}"
            }
        }

        stage('Deploy to Apache Directory') {
            steps {
                sh """
                    sudo cp -r * ${DEPLOY_DIR}/
                    sudo chmod -R 777 ${DEPLOY_DIR}
                """
            }
        }

        stage('Restart Apache Properly') {
            steps {
                sh '''
                    sudo pkill -f httpd || true
                    sleep 2
                    ps aux | grep httpd
                    sudo systemctl start httpd
                    sudo systemctl status httpd
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful!"
        }
        failure {
            echo "❌ Deployment failed. Check logs."
        }
    }
}
