pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install') {
            steps {
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        
        stage('Test') {
            steps {
                // no real tests—just a syntax check
                sh './venv/bin/python -m py_compile app.py'
            }
        }
        stage('Build & Archive') {
            steps {
                archiveArtifacts artifacts: 'app.py', fingerprint: true
            }
        }
    }
    post {
        success {
            echo "Pipeline succeeded on branch ${env.BRANCH_NAME}!"
        }
        failure {
            echo "Pipeline failed on branch ${env.BRANCH_NAME}!"
        }
    }
}

