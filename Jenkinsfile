pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Executing Build: Cleaning and packaging the project using Maven.'
            }
            post {
                always {
                    mail to: 'Johnnerojunior@gmail.com',
                         subject: "Build Stage Completed: ${currentBuild.fullDisplayName}",
                         body: "The Build stage finished with status: ${currentBuild.currentResult}. Please review the logs."
                }
            }
        }

        stage('Testing') {
            steps {
                echo 'Executing Testing: Running tests with Maven.'
            }
            post {
                always {
                    mail to: 'Johnnerojunior@gmail.com',
                         subject: "Testing Stage Completed: ${currentBuild.fullDisplayName}",
                         body: "The Testing stage finished with status: ${currentBuild.currentResult}. Please review the logs."
                }
            }
        }

        stage('Quality Analysis') {
            steps {
                echo 'Performing Quality Analysis: Checking code quality using Checkstyle.'
            }
            post {
                always {
                    mail to: 'Johnnerojunior@gmail.com',
                         subject: "Quality Analysis Completed: ${currentBuild.fullDisplayName}",
                         body: "The Quality Analysis stage finished with status: ${currentBuild.currentResult}. Please review the logs."
                }
            }
        }

        stage('Security Check') {
            steps {
                echo 'Running Security Check: Conducting a security scan using OWASP Dependency-Check.'
            }
            post {
                always {
                    mail to: 'Johnnerojunior@gmail.com',
                         subject: "Security Check Completed: ${currentBuild.fullDisplayName}",
                         body: "The Security Check stage finished with status: ${currentBuild.currentResult}. Please review the logs."
                }
            }
        }

        stage('Staging Deployment') {
            steps {
                echo 'Deploying to Staging: Executing deployment instructions for the staging environment.'
            }
            post {
                always {
                    mail to: 'Johnnerojunior@gmail.com',
                         subject: "Staging Deployment Completed: ${currentBuild.fullDisplayName}",
                         body: "The Staging Deployment stage finished with status: ${currentBuild.currentResult}. Please review the logs."
                }
            }
        }

        stage('Staging Tests') {
            steps {
                echo 'Running Staging Tests: Executing integration tests on the staging environment.'
            }
            post {
                always {
                    mail to: 'Johnnerojunior@gmail.com',
                         subject: "Staging Tests Completed: ${currentBuild.fullDisplayName}",
                         body: "The Staging Tests stage finished with status: ${currentBuild.currentResult}. Please review the logs."
                }
            }
        }

        stage('Production Deployment') {
            steps {
                echo 'Deploying to Production: Executing deployment instructions for the production environment.'
            }
            post {
                always {
                    mail to: 'Johnnerojunior@gmail.com',
                         subject: "Production Deployment Completed: ${currentBuild.fullDisplayName}",
                         body: "The Production Deployment stage finished with status: ${currentBuild.currentResult}. Please review the logs."
                }
            }
        }
    }

    post {
        always {
            mail to: 'Johnnerojunior@gmail.com',
                 subject: "Pipeline Execution Summary: ${currentBuild.fullDisplayName}",
                 body: "The complete pipeline execution has finished with status: ${currentBuild.currentResult}. Please review the logs."
        }
    }
}
