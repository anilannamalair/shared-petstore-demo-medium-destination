pipeline {
    agent any

    environment {
        MVN_CMD = 'mvn'
        RECIPIENTS = 'anilannamalair@gmail.com'
        EMAIL_SENDER = 'anilannamalair@gmail.com'
        JOB_NAME = 'CI Pipeline'
        BUILD_NUMBER = "${env.BUILD_NUMBER}"
        SMTP_SERVER = 'smtp.gmail.com'
        SMTP_PORT = '465'
        EMAIL_USERNAME = credentials('EMAIL_USERNAME') // Jenkins secret ID
        EMAIL_PASSWORD = credentials('EMAIL_PASSWORD') // Jenkins secret ID
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependency') {
            steps {
                sh "${env.MVN_CMD} clean install"
            }
        }

        stage('Build') {
            steps {
                sh "${env.MVN_CMD} clean package -DskipTests"
            }
        }

        stage('Test') {
            steps {
                sh "${env.MVN_CMD} test"
            }
        }

        stage('Lint') {
            steps {
                echo "Running lint checks..."
            }
        }

        stage('Code Quality') {
            steps {
                echo "Running code quality checks..."
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying..."
            }
        }
    }

    post {
        success {
            echo "Sending success email..."
            sh '''
                curl --verbose --url "smtps://${SMTP_SERVER}:${SMTP_PORT}" --ssl-reqd \
                    --mail-from "${EMAIL_SENDER}" \
                    --mail-rcpt "${RECIPIENTS}" \
                    --upload-file <(echo -e "From: ${EMAIL_SENDER}\\nTo: ${RECIPIENTS}\\nSubject: SUCCESS: Job ${JOB_NAME} [${BUILD_NUMBER}]\\n\\nJob ${JOB_NAME} [${BUILD_NUMBER}] succeeded.") \
                    --user "${EMAIL_USERNAME}:${EMAIL_PASSWORD}"
            '''
        }
    }
}
