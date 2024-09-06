pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Task: Build - Print Maven clean and package steps'
                bat 'echo mvn clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Task: Test - Print Maven test steps'
                bat 'echo mvn test > test.log' // Simulating log generation
            }
            post {
                success {
                    echo 'Task: Success Notification - Send email on Test stage success'
                    emailext to: 'johnnerojunior@gmail.com',
                            subject: "Test Stage Successful: ${currentBuild.fullDisplayName}",
                            body: "The Test stage completed successfully.",
                            attachLog: true,
                            attachmentsPattern: 'test.log'
                }
                failure {
                    echo 'Task: Failure Notification - Send email on Test stage failure'
                    emailext to: 'johnnerojunior@gmail.com',
                            subject: "Test Stage Failed: ${currentBuild.fullDisplayName}",
                            body: "The Test stage failed. Please check the logs.",
                            attachLog: true,
                            attachmentsPattern: 'test.log'
                }
            }
        }
        stage('Code Quality Check') {
            steps {
                echo 'Task: Code Quality Check - Print code quality analysis steps'
                bat 'echo Running code analysis > code_analysis.log' // Simulating log generation
            }
            post {
                success {
                    echo 'Task: Success Notification - Send email on Code Quality Check success'
                    emailext to: 'johnnerojunior@gmail.com',
                            subject: "Code Quality Check Successful: ${currentBuild.fullDisplayName}",
                            body: "The Code Quality Check completed successfully.",
                            attachLog: true,
                            attachmentsPattern: 'code_analysis.log'
                }
                failure {
                    echo 'Task: Failure Notification - Send email on Code Quality Check failure'
                    emailext to: 'johnnerojunior@gmail.com',
                            subject: "Code Quality Check Failed: ${currentBuild.fullDisplayName}",
                            body: "The Code Quality Check failed. Please check the logs.",
                            attachLog: true,
                            attachmentsPattern: 'code_analysis.log'
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Task: Security Scan - Print OWASP Dependency Check steps'
                bat 'echo Running security scan > security_scan.log' // Simulating log generation
            }
            post {
                success {
                    echo 'Task: Success Notification - Send email on Security Scan success'
                    emailext to: 'johnnerojunior@gmail.com',
                            subject: "Security Scan Successful: ${currentBuild.fullDisplayName}",
                            body: "The Security Scan completed successfully.",
                            attachLog: true,
                            attachmentsPattern: 'security_scan.log'
                }
                failure {
                    echo 'Task: Failure Notification - Send email on Security Scan failure'
                    emailext to: 'johnnerojunior@gmail.com',
                            subject: "Security Scan Failed: ${currentBuild.fullDisplayName}",
                            body: "The Security Scan failed. Please check the logs.",
                            attachLog: true,
                            attachmentsPattern: 'security_scan.log'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Task: Deploy to Staging - Print deployment steps to staging'
                bat 'echo Deploying to staging > deploy_staging.log' // Simulating log generation
            }
            post {
                success {
                    echo 'Task: Success Notification - Send email on Deploy to Staging success'
                    emailext to: 'johnnerojunior@gmail.com',
                            subject: "Staging Deployment Successful: ${currentBuild.fullDisplayName}",
                            body: "The deployment to staging completed successfully.",
                            attachLog: true,
                            attachmentsPattern: 'deploy_staging.log'
                }
                failure {
                    echo 'Task: Failure Notification - Send email on Deploy to Staging failure'
                    emailext to: 'johnnerojunior@gmail.com',
                            subject: "Staging Deployment Failed: ${currentBuild.fullDisplayName}",
                            body: "The deployment to staging failed. Please check the logs.",
                            attachLog: true,
                            attachmentsPattern: 'deploy_staging.log'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Task: Integration Tests - Print integration tests steps on staging'
                bat 'echo Running integration tests on staging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Task: Deploy to Production - Print production deployment steps'
                bat 'echo Deploying to production'
            }
        }
    }

    post {
        always {
            echo 'Task: Post-Pipeline Notification - Send final pipeline status email'
            emailext to: 'johnnerojunior@gmail.com',
                    subject: "Pipeline Status: ${currentBuild.fullDisplayName}",
                    body: "The pipeline has finished with status: ${currentBuild.currentResult}. Please check the logs.",
                    attachLog: true,
                    attachmentsPattern: '**/*.log' // Attaches all log files generated
        }
    }
}
