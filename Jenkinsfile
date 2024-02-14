pipeline {
    agent any
    tools {
        maven 'Maven 3.2.5'
    }

    stages {
        stage('Compile') {
            steps {
                // Compile the Maven project
                sh 'mvn compile'
            }
        }
        stage('Code') {
            steps {
                echo "code stage"
            }
        }
        stage('Review') {
            steps {

                echo "review stage"
                // Perform manual or automated code review
            }
        }
        stage('Unit Test') {
            steps {
                // Run unit tests
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                // Package the application into a WAR file
                sh 'mvn package'
            }
            post {
                success {
                    // Archive the WAR file as a build artifact
                    archiveArtifacts artifacts: 'target/*.war', fingerprint: true
                }
            }
        }
        stage('Deploy') {
            environment {
                TOMCAT_URL = 'http://localhost:8081/' // Replace with your Tomcat URL
                TOMCAT_CREDENTIALS_ID = 'tomcat-credentials' // ID of Jenkins credentials for Tomcat
            }
            steps {
                // Deploy the WAR file to Tomcat
                withCredentials([usernamePassword(credentialsId: "${TOMCAT_CREDENTIALS_ID}", usernameVariable: 'admin', passwordVariable: 'Upes@123')]) {
                    sh "curl -u ${TOMCAT_USERNAME}:${TOMCAT_PASSWORD} --upload-file target/*.war ${TOMCAT_URL}/manager/text/deploy?path=/my-webapp"
                }
            }
        }
    }
}
