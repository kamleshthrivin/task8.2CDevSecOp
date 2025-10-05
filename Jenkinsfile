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
                // Windows shell command
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                // Run tests, continue even if they fail
                bat 'npm test || exit 0'
            }
        }
        stage('Generate Coverage Report') {
            steps {
                // Generate coverage report, continue on failure
                bat 'npm run coverage || exit 0'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                // Run npm audit and continue despite errors
                bat 'npm audit || exit 0'
            }
        }
    }
}
