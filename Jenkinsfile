pipeline {
    agent any 

    triggers {
        // Trigger the pipeline on GitHub push events
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Run build commands here (e.g., install dependencies)
                echo 'Building the project...'
                sh 'python -m pip install -r requirements.txt'
                // Add additional build commands as needed
            }
        }

        stage('Test') {
            steps {
                // Run tests (this could be unit tests, integration tests, etc.)
                echo 'Running tests...'
                sh 'pytest'  // Adjust according to your testing framework
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application (could be to a server, container, etc.)
                echo 'Deploying application...'
                // Add your deployment commands here
            }
        }
    }

    post {
        success {
            // Email notification on successful build
            mail to: 'recipient@example.com',
                 subject: "Successful Build: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Good job! The build was successful. Check it out at ${env.BUILD_URL}."
        }
        failure {
            // Email notification on build failure
            mail to: 'recipient@example.com',
                 subject: "Failed Build: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build failed. Check the logs at ${env.BUILD_URL}."
        }
    }
}
