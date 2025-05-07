pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: ' https://github.com/sh4mbhavi/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0' 
            }
            post {
                always {
                    emailext(
                        to: 'dummyemailforjenkins@gmail.com',
                        subject: "Jenkins Build: 'Run Tests' - ${currentBuild.result}",
                        body: """The 'Run Tests' stage is finished.
                        Status: ${currentBuild.result}
                        Build Number: ${currentBuild.number}
                        Build URL: ${env.BUILD_URL}
                        Check the attached log for details.""",
                        attachLog: true
                    )
                }
            }
        }
        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
            post {
                always {
                    emailext(
                        to: 'dummyemailforjenkins@gmail.com',
                        subject: "Jenkins Build: 'NPM Audit (Security Scan)' - ${currentBuild.result}",
                        body: """The 'NPM Audit (Security Scan)' stage is finished.
                        Status: ${currentBuild.result}
                        Build Number: ${currentBuild.number}
                        Build URL: ${env.BUILD_URL}
                        Check the attached log for details.""",
                        attachLog: true
                    )
                }
            }
        }
    }
} 