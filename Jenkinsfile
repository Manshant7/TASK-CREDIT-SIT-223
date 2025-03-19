pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = "manshantdh.1@gmail.com"
        GIT_REPO = 'https://github.com/Manshant7/TASK-CREDIT-SIT-223.git'
        BRANCH = 'main'
    }

    triggers {
        githubPush()  //commit1
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the repository...'
                git branch: "${BRANCH}", url: "${GIT_REPO}" //commit2
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application using a build automation tool like Maven/Gradle.'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests using JUnit/TestNG for unit testing and Selenium/Cypress for integration testing.'
            }
            post {
                always {
                    echo "Sending test results via email..."
                    mail(
                        to: "${EMAIL_RECIPIENT}",
                        subject: "Test Stage Result - ${currentBuild.fullDisplayName}",
                        body: "Tests completed: ${currentBuild.currentResult}\n\nCheck Jenkins logs for details."
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis using SonarQube or CodeClimate.'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan using tools like OWASP Dependency-Check or Trivy.'
            }
            post {
                always {
                    echo "Sending security scan results via email..."
                    mail(
                        to: "${EMAIL_RECIPIENT}",
                        subject: "Security Scan Result - ${currentBuild.fullDisplayName}",
                        body: "Security scan completed: ${currentBuild.currentResult}\n\nCheck Jenkins logs for details."
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to Staging using Docker/Kubernetes/AWS EC2.'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests using Selenium/Postman on staging environment.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production using Ansible/Terraform for infrastructure automation.'
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed. Sending final status email..."
            mail(
                to: "${EMAIL_RECIPIENT}",
                subject: "Pipeline Execution Result - ${currentBuild.fullDisplayName}",
                body: "Pipeline finished with status : ${currentBuild.currentResult}\n\nCheck Jenkins logs for more details."
            )
        }
    }
}
