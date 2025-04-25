pipeline {
    agent any

    environment {
        MVN_CMD = 'mvn'
        RECIPIENTS = 'anilannamalair@gmail.com'
        EMAIL_SENDER = 'anilannamalair@gmail.com'
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main', url: 'https://github.com/anilannamalair/shared-petstore-demo-medium.git'
            }
        }

        stage('Install Dependency') {
            steps {
                sh "${MVN_CMD} clean install"
            }
        }

        stage('Build') {
            steps {
                sh "${MVN_CMD} clean package -DskipTests"
            }
        }

        stage('Test') {
            steps {
                sh "${MVN_CMD} test"
            }
        }

        stage('Lint') {
            steps {
                sh 'echo "Running lint checks..."'
                // Add your linting commands here
            }
        }

        stage('Code Quality') {
            steps {
                sh 'echo "Running code quality checks..."'
                // Add your code quality check commands here
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Deploying..."' // Replace with your deployment steps
            }
        }
    }

    post {
        success {
            emailext to: "${RECIPIENTS}",
                     from: "${EMAIL_SENDER}",
                     subject: "SUCCESS: Job \"${env.JOB_NAME} [${env.BUILD_NUMBER}]\"",
                     body: "Job \"${env.JOB_NAME} [${env.BUILD_NUMBER}]\" succeeded."
        }
        failure {
            emailext to: "${RECIPIENTS}",
                     from: "${EMAIL_SENDER}",
                     subject: "FAILURE: Job \"${env.JOB_NAME} [${env.BUILD_NUMBER}]\"",
                     body: "Job \"${env.JOB_NAME} [${env.BUILD_NUMBER}]\" failed."
        }
        always {
            cleanWs()
        }
    }
}
