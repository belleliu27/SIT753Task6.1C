pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building the project"
                // You can include actual build commands here
            }
        }
    }

    post {
        success {
            emailext body: 'The build was successful. Logs are attached.',
                     subject: 'Build Successful',
                     to: 'michaelzj23@gmail.com'
        }
        failure {
            emailext body: 'The build failed. Please check the logs for details.',
                     subject: 'Build Failed',
                     to: 'michaelzj23@gmail.com'
        }
    }
}
