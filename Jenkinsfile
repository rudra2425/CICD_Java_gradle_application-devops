pipeline {
    agent any

    stages {
        stage('SonarQube Quality Check') {
            agent {
                docker {
                    image 'openjdk:11'
                }
            }
            steps {
                // Ensure Gradle Wrapper has execute permissions
                sh 'chmod +x gradlew'

                // Run SonarQube analysis
                withSonarQubeEnv(credentialsId: 'sonar-token') {
                    sh './gradlew sonarqube'
                }
            }
        }
    }
}
