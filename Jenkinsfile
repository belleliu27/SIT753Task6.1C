pipeline {
    agent any

tools {
        maven 'Maven 3.9.9'  // The name you specified in the Maven configuration
    }
    stages {
        stage('Build') {
            steps {
                script {
                    // Example build tool: Maven
                    sh 'mvn clean package'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Example test tools: JUnit, TestNG
                    sh 'mvn test'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    // Example code analysis tool: SonarQube
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    // Example security scan tool: OWASP Dependency-Check
                    sh 'dependency-check.sh --project my-project'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    // Example deployment: AWS CLI
                    sh 'aws s3 cp my-app.jar s3://my-staging-bucket/'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Example test tool: Postman for API tests
                    sh 'newman run my-api-tests.postman_collection.json'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    // Example deployment: AWS CLI
                    sh 'aws s3 cp my-app.jar s3://my-production-bucket/'
                }
            }
        }
    }

    post {
        success {
            emailext(
                to: 'michaelzj23@gmail.com',
                subject: 'Build Successful',
                body: 'The build was successful. Please find the attached logs.',
               
            )
        }
        failure {
            emailext(
                to: 'michaelzj23@gmail.com',
                subject: 'Build Failed',
                body: 'The build failed. Please find the attached logs.',
               
            )
        }
    }
}
