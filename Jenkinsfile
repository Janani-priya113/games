pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Janani-priya113/games.git'
            }
        }
        stage('Deploy to Docker Container') {
            steps {
                script {
                    // Copy 'new' file into the Apache container
                    sh 'docker cp new deploy_container:/var/www/html/index.html'
                    // Gracefully reload Apache without killing the container
                    sh 'docker exec deploy_container apachectl -k graceful || true'
                }
            }
        }
    }
}

