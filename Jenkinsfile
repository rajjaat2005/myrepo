pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'git@github.com:rajjaat2005/myrepo.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                mkdir -p /var/www/myweb
                cp -r * /var/www/myweb/
                echo "Website deployed successfully!"
                '''
            }
        }
    }
}

