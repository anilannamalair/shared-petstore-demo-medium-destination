pipeline {

    agent any



    stages {

		stage('install dependency') {

            steps {

                sh 'mvn clean install' // Example for a Maven project

            }

        }
       

        stage('Build') {

            steps {

                sh 'mvn clean install -DskipTests' // Example for a Maven project

            }

        }

        stage('Test') {

            steps {

                sh 'mvn test' // Example for a Maven project

            }

        }

        stage('Deploy') {

            steps {

                sh 'echo "Deploying..."' // Replace with your deployment steps

            }

        }

    }

} 
