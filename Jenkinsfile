pipeline {
    agent any

    environment {
        VENV_DIR = 'venv'
    }

  stage('Checkout') {
    steps {
        echo 'Checking out source code...'
        git branch: 'main', url: 'https://github.com/Aditya-Firedrake/Python-jenkins.git'
    }
}


        stage('Set Up Python Env') {
            steps {
                echo 'Creating virtual environment...'
                sh 'python3 -m venv $VENV_DIR'
                sh './$VENV_DIR/bin/pip install --upgrade pip'
                sh './$VENV_DIR/bin/pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests with pytest...'
                sh './$VENV_DIR/bin/python -m pytest'
            }
        }
    }

    post {
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}
