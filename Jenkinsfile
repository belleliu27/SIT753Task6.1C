pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building the project"
                // Tool: Maven
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit and integration tests"
                // Tool: JUnit (or any other test automation tool)
                sh 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo "Performing code analysis"
                // Tool: SonarQube
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo "Performing security scan"
                // Tool: OWASP Dependency-Check
                sh 'dependency-check --project MyProject --scan .'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging environment"
                // Tool: AWS CLI (for deployment)
                sh 'aws s3 cp target/myapp.jar s3://my-staging-bucket/'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging"
                // Tool: Selenium (or any other integration testing tool)
                sh 'mvn verify'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo "Deploying to production environment"
                // Tool: AWS CLI (for deployment)
                sh 'aws s3 cp target/myapp.jar s3://my-production-bucket/'
            }
        }
    }

    post {
        success {
            emailext body: 'Pipeline succeeded. Build and test details attached.', 
                     subject: 'Build Success', 
                     to: 'michaelzj23@gmail.com',
                     attachLog: true
        }
        failure {
            emailext body: 'Pipeline failed. Check the logs for details.', 
                     subject: 'Build Failure', 
                     to: 'michaelzj23@gmail.com',
                     attachLog: true
        }
    }
}
