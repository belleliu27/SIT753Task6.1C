pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9' // Ensure this matches the name you configured in Jenkins
        dependencyCheck 'DC' // Ensure this matches the name you configured in Jenkins
    }

    stages {
        stage('Build') {
            steps {
                echo "Building the project"
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit and integration tests"
                sh 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo "Performing code analysis"
                sh 'mvn sonar:sonar -Dsonar.login=squ_cd3bc3e512163d412e69c8a3d406d1574d50e0a9'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo "Performing security scan"
                sh 'dependency-check --project MyProject --scan .'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging environment"
                sh 'aws s3 cp target/myapp.jar s3://my-staging-bucket/'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging"
                sh 'mvn verify'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo "Deploying to production environment"
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
