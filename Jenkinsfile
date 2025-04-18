pipeline {
    agent any

    environment {
        VENV = "${env.WORKSPACE}/venv"
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
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install --upgrade pip'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
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
