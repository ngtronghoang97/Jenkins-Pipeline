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
                    // Send email notification on test failure
                    emailext(
                        subject: "Testing - Failure ${currentBuild.fullDisplayName}",
                        body: "The Test stage has failed.",
                        to: "15520260@gm.uit.edu.vn",
                        attachmentsPattern: "*.log"
                    )
                }
                success {
                    // Send email notification on test success
                    emailext(
                        subject: "Testing - Success ${currentBuild.fullDisplayName}",
                        body: "The Test stage has completed successfully.",
                        to: "15520260@gm.uit.edu.vn",
                        attachmentsPattern: "*.log"
                    )
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
			/*post {
                success {
                    // Send email notification on test success
                    emailext(
                        subject: "Security Scan - Success ${currentBuild.fullDisplayName}",
                        body: "The Security Scan stage has completed successfully.",
                        to: "15520260@gm.uit.edu.vn",
                        attachLog: true,
                        mimeType: 'text/plain'
                    )
                }
                failure {
                    // Send email notification on test failure
                    emailext(
                        subject: "Security Scan - Failure ${currentBuild.fullDisplayName}",
                        body: "The Security Scan stage has failed.",
                        to: "15520260@gm.uit.edu.vn",
                        attachLog: true,
                        mimeType: 'text/plain'
                    )
                }
            }*/
            post{
                failure {
                    mail to: "15520260@gm.uit.edu.vn",
                    subject: "Security Scan - Failure ${currentBuild.fullDisplayName}",
                    body: "The Security Scan stage has failed.",
                }
                success {
                    emailext attachLog: true,
                    mimeType: 'text/plain'
                    mail to: "15520260@gm.uit.edu.vn",
                    subject: "Security Scan - Success ${currentBuild.fullDisplayName}",
                    body: "The Security Scan stage has completed successfully.",
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
