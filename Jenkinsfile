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
                venv\\Scripts\\python.exe -m pip install --upgrade pip
                venv\\Scripts\\python.exe -m pip install -r requirements.txt
                venv\\Scripts\\python.exe -m pip install pytest
                '''
            }
        }   

        stage('Run Unit Tests') {
            steps {
                bat '''
                venv\\Scripts\\python.exe -m pytest
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
