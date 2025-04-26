pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = "manshantdh.1@gmail.com"
        GIT_REPO = 'https://github.com/Manshant7/TASK-CREDIT-SIT-223.git'
        BRANCH = 'main'
    }

    triggers {
        pollSCM('* * * * *')//check every minute

    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Task: Cloning the repository to fetch the latest codebase.'
                echo 'Tool: Git'
                git branch: "${BRANCH}", url: "${GIT_REPO}" 
            }
        }

        stage('Build') {
            steps {
                echo 'Task: Compiling the source code and resolving dependencies.'
                echo 'Tool: Maven or Gradle'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Task: Running unit and integration tests to validate code functionality.'
                echo 'Tools: JUnit/TestNG for unit tests, Selenium/Cypress for integration tests'
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
                echo 'Task: Performing static code analysis to ensure code quality and adherence to standards.'
                echo 'Tool: SonarQube or CodeClimate'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Task: Scanning for security vulnerabilities in dependencies and code.'
                echo 'Tools: OWASP Dependency-Check, Trivy'
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
                echo 'Task: Deploying the application to a staging environment for further testing.'
                echo 'Tools: Docker, Kubernetes, AWS EC2'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Task: Running end-to-end integration tests in the staging environment.'
                echo 'Tools: Selenium, Postman'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Task: Deploying the application to the production environment.'
                echo 'Tools: Ansible, Terraform'
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
