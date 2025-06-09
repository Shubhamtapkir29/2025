pipeline {
    agent { label 'arpita-slave' }

    environment {
        DEPLOY_DIR = "/var/www/deploy"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: '2025Q1', url: 'https://github.com/Shubhamtapkir29/2025.git'
            }
        }

        stage('Clean Deploy Directory') {
            steps {
                sh '''
                echo "🧹 Cleaning old content in $DEPLOY_DIR"
                sudo rm -rf ${DEPLOY_DIR}/*
                sudo mkdir -p ${DEPLOY_DIR}
                '''
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                echo "🚀 Starting Apache"
                sudo pkill -f httpd || true
                sudo systemctl start httpd
                sudo chmod -R 755 ${DEPLOY_DIR}
                sudo cp -r * ${DEPLOY_DIR}/
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment from '2025Q1' branch successful!"
        }
        failure {
            echo "❌ Deployment failed. Check the logs above."
        }
    }
}
