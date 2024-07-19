pipeline {
    agent any

    environment {
        // Define environment variables
        SONARQUBE_URL = 'http://54.160.179.28:9000'
        SONARQUBE_TOKEN = credentials('sonar-token') // Replace with your SonarQube token ID
        
    }

    stages {
<<<<<<< HEAD
        stage('Checkout') {
            steps {
                // Checkout code from the version control system
                git 'https://github.com/rudra2425/CICD_Java_gradle_application-devops.git'
            }
        }

        stage('Build') {
            steps {
                // Build the project using Gradle
                script {
                    sh './gradlew clean build'
=======
        stage('SonarQube Quality Check') {
            agent {
                docker {
                    image 'openjdk:11'
>>>>>>> 6f0a22ee46757ebaaf883e2797bce926fdc7ffea
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
<<<<<<< HEAD
                // Run SonarQube analysis
                script {
                    sh './gradlew sonarqube -Dsonar.projectKey=your-project-key -Dsonar.host.url=${SONARQUBE_URL} -Dsonar.login=${SONARQUBE_TOKEN}'
                }
            }
        }

        stage('Upload to Nexus') {
            steps {
                script {
                    // Define the artifact to upload
                    def jarFile = 'build/libs/your-app.jar'
                    
                    // Upload the artifact to Nexus
                    sh '''
                        curl -v -u ${NEXUS_CRED_USR}:${NEXUS_CRED_PSW} --upload-file ${jarFile} ${NEXUS_URL}/repository/${NEXUS_REPO}/your-app.jar
                    '''
=======
                  script{
                      withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'chmod +x gradlew'
                        sh './gradlew sonarqube'
                    }
>>>>>>> 6f0a22ee46757ebaaf883e2797bce926fdc7ffea
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
