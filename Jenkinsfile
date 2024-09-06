pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Task: Build - Using Maven to clean and package the project'
                // Example build step
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Task: Test - Using Maven to run tests'
                // Example test step
                sh 'mvn test > test.log'
            }
            post {
                success {
                    mail to: 'johnnerojunior@gmail.com',
                         subject: "Pipeline Success: ${currentBuild.fullDisplayName}",
                         body: "The Test stage of the pipeline has succeeded. Please find the log attached.",
                         attachmentsPattern: 'test.log'
                }
                failure {
                    mail to: 'johnnerojunior@gmail.com',
                         subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                         body: "The Test stage of the pipeline has failed. Please find the log attached.",
                         attachmentsPattern: 'test.log'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Task: Code Analysis - Performing code quality analysis'
                // Code analysis step (replace with actual command)
                sh 'mvn sonar:sonar > code_analysis.log'
            }
            post {
                always {
                    mail to: 'johnnerojunior@gmail.com',
                         subject: "Code Analysis Stage Completed: ${currentBuild.fullDisplayName}",
                         body: "The Code Analysis stage has finished. Check the attached log for details.",
                         attachmentsPattern: 'code_analysis.log'
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Task: Security Scan - Performing security scan'
                // Security scan step (replace with actual command)
                sh 'dependency-check.sh --project my-app --scan ./ > security_scan.log'
            }
            post {
                always {
                    mail to: 'johnnerojunior@gmail.com',
                         subject: "Security Scan Stage Completed: ${currentBuild.fullDisplayName}",
                         body: "The Security Scan stage has finished. Check the attached log for details.",
                         attachmentsPattern: 'security_scan.log'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Task: Deploy to Staging - Deploying to staging environment'
                // Example deploy step (replace with actual command)
                sh 'scp target/my-app.jar user@staging-server:/path/to/deploy/ > deploy_staging.log'
            }
            post {
                always {
                    mail to: 'johnnerojunior@gmail.com',
                         subject: "Deploy to Staging Completed: ${currentBuild.fullDisplayName}",
                         body: "Deployment to staging has finished. Check the attached log for details.",
                         attachmentsPattern: 'deploy_staging.log'
                }
            }
        }
    }

    post {
        always {
            mail to: 'johnnerojunior@gmail.com',
                 subject: "Pipeline ${currentBuild.fullDisplayName} Completed",
                 body: "The entire pipeline has finished with status: ${currentBuild.currentResult}. Please check the logs for more details.",
                 attachmentsPattern: '**/*.log'
        }
    }
}
