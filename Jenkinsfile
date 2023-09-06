pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    userRemoteConfigs: [[url: 'https://github.com/akramdevopstrainer/maven-standalone-application.git']]
                ])
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Testing') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Rename JAR to WAR') {
            steps {
                sh 'cp target/maven-stanalone-application-0.0.1-SNAPSHOT.jar target/maven-standalone-application-0.0.1-SNAPSHOT.war'
            }
        }

        // Add more stages for deployment or other tasks as needed.
    }

    post {
        success {
            echo 'Build and tests succeeded! Deploying...'
            // Add deployment steps here.
        }

        failure {
            echo 'Build or tests failed. Notify the team.'
            // Add notification or rollback steps here.
        }
    }
}
