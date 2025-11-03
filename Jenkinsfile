pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                git branch: 'master', url: 'https://github.com/rajjaat2005/myrepo.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building project...'
                sh 'echo "Build step completed successfully"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to web server...'
                sh '''
                    sudo rm -rf /var/www/html/*
                    sudo cp -r * /var/www/html/
                    sudo systemctl restart nginx
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful! ✅'
        }
        failure {
