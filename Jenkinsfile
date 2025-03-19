pipeline {
    agent any

    environment {
        MVN_CMD = 'mvn'
    }

    stages {
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

        stage('Deploy') {
            steps {
                sh 'echo "Deploying..."' // Replace with your deployment steps
            }
        }
    }

    post {
        success {
            mail to: 'team@example.com',
                 subject: "SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                 body: "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' succeeded."
        }
        failure {
            mail to: 'team@example.com',
                 subject: "FAILURE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                 body: "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' failed."
        }
        always {
            cleanWs()
        }
    }
}
