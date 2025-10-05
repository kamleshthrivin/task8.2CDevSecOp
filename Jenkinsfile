pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/kamleshthrivin/task8.2CDevSecOp.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                
                bat 'npm test || exit 0'
            }
        }
        stage('Generate Coverage Report') {
            steps {
                
                bat 'npm run coverage || exit 0'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                
                bat 'npm audit || exit 0'
            }
        }
    }
}
