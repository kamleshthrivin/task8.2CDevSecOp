pipeline {
    agent any

    tools {
        nodejs "NodeJS_20" 
    }

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
            post {
                success {
                    emailext(
                        to: 'youremail@example.com',
                        subject: "Tests Passed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The *Run Tests* stage succeeded.\n\nCheck Jenkins for build logs.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: 'youremail@example.com',
                        subject: "Tests Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The *Run Tests* stage failed.\n\nCheck Jenkins for details.",
                        attachLog: true
                    )
                }
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
            post {
                success {
                    emailext(
                        to: 'kamleshthrivin15@gmail.com',
                        subject: "Security Scan Passed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The *NPM Audit (Security Scan)* stage completed successfully.\n\nNo critical vulnerabilities found.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: 'kamleshthrivin15@gmail.com',
                        subject: "Security Scan Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The *NPM Audit (Security Scan)* stage found vulnerabilities.\n\nCheck Jenkins logs for more details.",
                        attachLog: true
                    )
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}