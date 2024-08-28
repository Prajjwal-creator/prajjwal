pipeline {
    agent any

    environment {
        // Define your environment variables if needed
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Use Maven as the build automation tool
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Use JUnit for unit testing and Postman/Newman for integration testing
                sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                // Use SonarQube as the code analysis tool
                sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Use OWASP Dependency-Check for security scanning
                sh 'mvn dependency-check:check'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // Deploy to AWS EC2 instance using a script or deployment tool
                sh 'scp target/my-app.jar ec2-user@staging-server:/path/to/deploy'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Run integration tests on the staging server
                sh 'ssh ec2-user@staging-server "cd /path/to/deploy && ./run-tests.sh"'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Deploy to the production server
                sh 'scp target/my-app.jar ec2-user@production-server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            echo 'Sending email notifications...'
            // Configure email notifications
            mail to: 'developer@example.com',
                subject: "Jenkins Pipeline: ${currentBuild.fullDisplayName}",
                body: "Pipeline ${currentBuild.fullDisplayName} finished with status ${currentBuild.currentResult}.",
                attachLog: true
        }
    }
}
