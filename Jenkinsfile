pipeline {
    agent any

    environment {
        PROJECT_DIR = "/home/ubuntu/myrepo"
        VENV_DIR = "/home/ubuntu/myrepo/venv"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:rajjaat2005/myrepo.git', credentialsId: 'jenkins-github-cicd'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh """
                source ${VENV_DIR}/bin/activate
                pip install -r ${PROJECT_DIR}/requirements.txt
                """
            }
        }

        stage('Migrate DB') {
            steps {
                sh """
                source ${VENV_DIR}/bin/activate
                python ${PROJECT_DIR}/manage.py migrate
                """
            }
        }

        stage('Collect Static') {
            steps {
                sh """
                source ${VENV_DIR}/bin/activate
                python ${PROJECT_DIR}/manage.py collectstatic --noinput
                """
            }
        }

        stage('Restart Gunicorn') {
            steps {
                sh "sudo systemctl restart gunicorn"
            }
        }
    }
}
