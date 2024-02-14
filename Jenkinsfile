pipeline {
    agent any

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
        
            steps {
                sh 'mvn install tomcat7:deploy'
            }
        }
    }
}
