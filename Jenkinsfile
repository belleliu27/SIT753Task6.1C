pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9' // Ensure this matches the name you configured in Jenkins
        
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
                echo 'Security scan helps identify vulnerabilities, weaknesses, and other security risks in codebases.'
                echo 'Veracode:'
                echo 'A scan which analyzes source code for security vulnerabilities without executing the code.'
                echo 'Identifies common security flaws like SQL injection, XSS, and hardcoded secrets.'

            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Refers to the process of deploying an application to a production or test environment.'
                echo 'AWS EC2 deploy:'
                echo 'A deployment service provided by AWS that automates deploying applications to EC2 instances.'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
               echo 'Integration testing is a crucial step in the software development lifecycle.'
                echo 'Aims to verify that different components or systems work together as expected.'
                echo 'Selenium: For automating browser-based tests, useful for testing web applications.'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploy the application to the production server from the staging server.'
                echo 'The same AWS EC2 instance can be used to deploy to the production server.'
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
