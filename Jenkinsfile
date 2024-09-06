pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Task: Build - Using Maven to clean and package the project'
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Task: Test - Using Maven to run tests'
                sh 'mvn test > test.log'
            }
            post {
                success {
                    emailext to: 'johnnerojunior@gmail.com',
                             subject: "Pipeline Success: ${currentBuild.fullDisplayName}",
                             body: "The Test stage of the pipeline has succeeded. Please find the log attached.",
                             attachLog: true,
                             attachmentsPattern: 'test.log'
                }
                failure {
                    emailext to: 'johnnerojunior@gmail.com',
                             subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                             body: "The Test stage of the pipeline has failed. Please find the log attached.",
                             attachLog: true,
                             attachmentsPattern: 'test.log'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Task: Code Analysis - Performing code quality analysis'
                sh 'mvn sonar:sonar > code_analysis.log'
            }
            post {
                always {
                    emailext to: 'johnnerojunior@gmail.com',
                             subject: "Code Analysis Stage Completed: ${currentBuild.fullDisplayName}",
                             body: "The Code Analysis stage has finished. Check the attached log for details.",
                             attachLog: true,
                             attachmentsPattern: 'code_analysis.log'
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Task: Security Scan - Performing security scan'
                sh 'dependency-check.sh --project my-app --scan ./ > security_scan.log'
            }
            post {
                always {
                    emailext to: 'johnnerojunior@gmail.com',
                             subject: "Security Scan Stage Completed: ${currentBuild.fullDisplayName}",
                             body: "The Security Scan stage has finished. Check the attached log for details.",
                             attachLog: true,
                             attachmentsPattern: 'security_scan.log'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Task: Deploy to Staging - Deploying to staging environment'
                sh 'scp target/my-app.jar user@staging-server:/path/to/deploy/ > deploy_staging.log'
            }
            post {
                always {
                    emailext to: 'johnnerojunior@gmail.com',
                             subject: "Deploy to Staging Completed: ${currentBuild.fullDisplayName}",
                             body: "Deployment to staging has finished. Check the attached log for details.",
                             attachLog: true,
                             attachmentsPattern: 'deploy_staging.log'
                }
            }
        }
    }

    post {
        always {
            emailext to: 'johnnerojunior@gmail.com',
                     subject: "Pipeline ${currentBuild.fullDisplayName} Completed",
                     body: "The entire pipeline has finished with status: ${currentBuild.currentResult}. Please check the logs for more details.",
                     attachLog: true,
                     attachmentsPattern: '**/*.log'
        }
    }
}
