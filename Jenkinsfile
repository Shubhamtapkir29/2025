pipeline {
    agent any

    stages {
        stage('Deploy') {
            steps {
                sh '''
                echo "Deploying from branch: ${BRANCH_NAME}"
                sudo pkill -f httpd || true
                sudo systemctl start httpd
                sudo chmod -R 777 /var/www/html
                sudo rsync -av --delete ./ /var/www/html/
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment from ${BRANCH_NAME} successful."
        }
        failure {
            echo "❌ Deployment from ${BRANCH_NAME} failed."
        }
    }
}
