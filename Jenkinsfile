pipeline {
    agent any

    environment {
        PROJECT_DIR = "/home/ubuntu/myrepo"
        VENV_DIR = "${PROJECT_DIR}/venv"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'jenkins-github-cicd',
                    url: 'git@github.com:rajjaat2005/myrepo.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                #!/bin/bash
                python3 -m venv ${VENV_DIR}
                source ${VENV_DIR}/bin/activate
                pip install --upgrade pip
                pip install -r ${PROJECT_DIR}/requirements.txt
                '''
            }
        }

        stage('Migrate Database') {
            steps {
                sh '''
                #!/bin/bash
                source ${VENV_DIR}/bin/activate
                cd ${PROJECT_DIR}
                python3 manage.py migrate
                '''
            }
        }

        stage('Collect Static Files') {
            steps {
                sh '''
                #!/bin/bash
                source ${VENV_DIR}/bin/activate
                cd ${PROJECT_DIR}
                python3 manage.py collectstatic --noinput
                '''
            }
        }

        stage('Restart Gunicorn') {
            steps {
                sh '''
                sudo systemctl restart gunicorn
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deploy successful'
        }
        failure {
            echo '❌ Deploy failed — check Jenkins logs'
        }
    }
}

