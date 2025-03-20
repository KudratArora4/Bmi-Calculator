pipeline {
    agent any

    environment {
        STAGING_ENV = 'AWS EC2'      //Staging environment --> example
        PRODUCTION_ENV = 'AWS EC2'  //Production environment --> example
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using npm install [Other Tools: Maven, Gradle, yarn]'
                //[Other Available Tools for various project types --> Maven, Gradle, yarn]
                
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using Jest'
                //[Other Available Tools for various project types -->  JUnit, TestNG, Mocha]
                
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/logs/*.log', fingerprint: true
                    mail to: 'kudratskarora@gmail.com',
                         subject: 'Unit and Integration Tests Passed - BMI Calculator',
                         body: 'The unit and integration tests completed successfully. Logs are available in Jenkins.'
                }
                failure {
                    archiveArtifacts artifacts: '**/logs/*.log', fingerprint: true
                    mail to: 'kudratskarora@gmail.com',
                         subject: 'Unit and Integration Tests Failed - BMI Calculator',
                         body: 'The unit and integration tests failed. Please check the logs in Jenkins.'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                  echo 'Performing code analysis using SonarQube'
                  //[Other Available Tools for various project types --> ESLint, Checkstyle]
                  sh 'echo "Code analysis completed" > logs/code_analysis.log'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
                //[Other Available Tools for various project types --> Snyk, Dependency-Check]
                sh 'echo "Security scan completed" > logs/security_scan.log'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/logs/*.log', fingerprint: true
                    mail to: 'kudratskarora@gmail.com',
                         subject: 'Security Scan Passed - BMI Calculator',
                         body: 'The security scan completed successfully. Logs are available in Jenkins.'
                }
                failure {
                    archiveArtifacts artifacts: '**/logs/*.log', fingerprint: true
                    mail to: 'kudratskarora@gmail.com',
                         subject: 'Security Scan Failed - BMI Calculator',
                         body: 'The security scan failed. Please check the logs in Jenkins.'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying application to staging environment using ${env.STAGING_ENV} "
                //[Other Available Tools for various project types --> Docker, Kubernetes]
                sh 'echo "Deployed to staging" > logs/deploy_staging.log'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment using Cypress'
                //[Other Available Tools for various project types --> Selenium, Postman, JMeter]
                sh 'echo "Integration tests on staging completed" > logs/integration_staging.log'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying application to production environment using ${env.PRODUCTION_ENV}"
                //[Other Available Tools for various project types --> Docker, Kubernetes, Azure App Services]
                sh 'echo "Deployed to production" > logs/deploy_production.log'
            }
        }
    }

    post {
        success {
            mail to: 'kudratskarora@gmail.com',
                 subject: 'Jenkins Pipeline Success - BMI Calculator',
                 body: 'The pipeline has completed successfully. Logs are available in Jenkins.'
        }
        failure {
            mail to: 'kudratskarora@gmail.com',
                 subject: 'Jenkins Pipeline Failure - BMI Calculator',
                 body: 'The pipeline has failed. Check Jenkins logs for details.'
        }
    }
}
