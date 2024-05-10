pipeline {
    agent any

    environment {
        DIRECTORY_PATH = 'Jenkins'
        TESTING_ENVIRONMENT = 'SIT753 Professional Practice in IT'
        PRODUCTION_ENVIRONMENT = 'AWS EC2'
	    BUILD_AUTOMATION = 'Maven'
	    STAGING_SERVER = 'AWS EC2'
	    SECURITY_SCAN = "OWASP ZAP"
    }

    stages {
        stage('Build') {
            steps {          
                echo "Build the source code using ${env.BUILD_AUTOMATION}"
                echo "Fetching the source code from the directory path specified by the environment variable ${env.DIRECTORY_PATH}."
                echo "Compiling the code and generating any necessary artifacts."
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests."
                echo "Running integration tests."
                echo "Unit tests and integration tests completed using ${env.TESTING_ENVIRONMENT}."
            }
            post{
                failure {
                    emailext subject: "TESTING STATUS - FAILURE",
                    to: "15520260@gm.uit.edu.vn",
                    body: "The pipeline testing status failed! Check the log attachment below",
                    attachLog: true
                }
                success {
                    emailext subject: "TESTING STATUS - SUCCESS",
                    to: "15520260@gm.uit.edu.vn",
                    body: "The pipeline testing status was successful! Check the log attachment below",
                    attachLog: true
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Integrating a code analysis tool."
            }
        }
        
        stage('Security Scan') {
            steps {
                echo "Performing a security scan on the code using a tool ${env.SECURITY_SCAN}."
            }
            post{
                failure {
                    emailext subject: "Security Scan - Failure ${currentBuild.fullDisplayName}",
                    to: "15520260@gm.uit.edu.vn",
                    body: "The Security Scan stage has failed.",
                    attachLog: true
                }
                success {
                    emailext subject: "Security Scan - Success ${currentBuild.fullDisplayName}",
                    to: "15520260@gm.uit.edu.vn",
                    body: "The Security Scan stage has completed successfully.",
                    attachLog: true
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to a staging server ${env.STAGING_SERVER}."
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment."
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying the code to the production environment ${env.PRODUCTION_ENVIRONMENT}."
            }
        }
    }
}