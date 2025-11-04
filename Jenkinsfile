pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/rajjaat2005/myrepo.git'
            }
        }

        stage('Deploy Website') {
            steps {
                echo 'Deploying website to /var/www/html ...'
                sh 'sudo cp -r * /var/www/html/'
                sh 'sudo systemctl restart nginx || true'
            }
        }
    }

    post {
        success {
            echo '🎉 Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}

