pipeline {
    agent any

    environment {
        CONTAINER_NAME = "deploy_container"
        APP_DIR = "/var/www/html"
    }

    stages {
        stage('Clone Code from GitHub') {
            steps {
                git 'https://github.com/Janani-priya113/games.git'
            }
        }

        stage('Copy File to Apache Container') {
            steps {
                script {
                    echo "Copying 'new' file to the container..."
                    sh "docker cp new ${CONTAINER_NAME}:${APP_DIR}/new"
                }
            }
        }

        stage('Restart Apache') {
            steps {
                script {
                    echo "Restarting Apache inside the container..."
                    sh "docker exec ${CONTAINER_NAME} service apache2 restart"
                }
            }
        }
    }

    post {
        success {
            echo "Deployed successfully! Check http://<your-ec2-ip>:3333"
        }
        failure {
            echo "Deployment failed. Check console output for errors."
        }
    }
}

