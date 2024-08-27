pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out the code from the repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build the project using Maven
                    sh 'echo "Building the project with Maven..."'
                    sh 'mvn clean package'  // Example: running a Maven build
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Run unit and integration tests using Maven
                    sh 'echo "Running unit and integration tests..."'
                    sh 'mvn test'  // Example: running tests with Maven
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    // Perform code analysis using a tool like SonarQube
                    sh 'echo "Performing code analysis with SonarQube..."'
                    sh 'mvn sonar:sonar'  // Example: running SonarQube analysis
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    // Perform a security scan using OWASP Dependency Check
                    sh 'echo "Running security scan with OWASP Dependency Check..."'
                    sh 'mvn org.owasp:dependency-check-maven:check'  // Example: running security scan
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    // Deploy the application to the staging environment
                    sh 'echo "Deploying to staging environment..."'
                    sh './deploy-staging.sh'  // Example: running a deployment script
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Run integration tests on the staging environment
                    sh 'echo "Running integration tests on staging environment..."'
                    sh './integration-tests-staging.sh'  // Example: running integration tests on staging
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    // Deploy the application to the production environment
                    sh 'echo "Deploying to production environment..."'
                    sh './deploy-production.sh'  // Example: running a production deployment script
                }
            }
        }
    }

    post {
        success {
            emailext
                to: 'michaelzj23@gmail.com',
                subject: 'Build Successful',
                body: 'The build and deployment pipeline was successful. Logs attached.',
                attachLog: true
            
        }
        failure {
            emailext
                to: 'michaelzj23@gmail.com',
                subject: 'Build Failed',
                body: 'The build and deployment pipeline failed. Logs attached.',
                attachLog: true
            
        }
    }
}
