pipeline {
    agent any

    environment {
        VENV = "${env.WORKSPACE}/venv"
        PYTHONPATH = "${env.WORKSPACE}"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                git branch: 'main', url: 'https://github.com/Aditya-Firedrake/Python-jenkins.git'
            }
        }

        stage('Set Up Python Env') {
            steps {
                echo 'Setting up Python environment...'
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install --upgrade pip'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh './venv/bin/pytest tests/'
            }
        }
    }

    post {
        failure {
            echo 'Build or tests failed.'
        }
    }
}
