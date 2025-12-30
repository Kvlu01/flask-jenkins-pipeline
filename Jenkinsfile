pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                echo 'Code already cloned by Jenkins from GitHub'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                python -m venv venv
                venv\\Scripts\\activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat '''
                venv\\Scripts\\activate
                pytest
                '''
            }
        }

        stage('Build Application') {
            steps {
                bat '''
                mkdir build
                copy app.py build\\
                copy requirements.txt build\\
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                bat '''
                mkdir C:\\flask_deployment
                xcopy build\\* C:\\flask_deployment\\ /E /Y
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
