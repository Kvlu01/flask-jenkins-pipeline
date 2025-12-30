pipeline {
    agent any

    environment {
        VENV = "venv"
        DEPLOY_DIR = "/tmp/flask_deployment"
    }

    stages {

        stage('Clone Repository') {
            steps {
                echo 'Code already cloned by Jenkins from GitHub'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv $VENV
                . $VENV/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '''
                . $VENV/bin/activate
                pytest
                '''
            }
        }

        stage('Build Application') {
            steps {
                sh '''
                mkdir -p build
                cp app.py requirements.txt build/
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                mkdir -p $DEPLOY_DIR
                cp -r build/* $DEPLOY_DIR
                echo "Application deployed to $DEPLOY_DIR"
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline executed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
