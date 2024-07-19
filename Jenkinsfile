pipeline {
    agent any

    environment {
        // Define environment variables
        SONARQUBE_URL = 'http://your-sonarqube-server'
        SONARQUBE_TOKEN = credentials('sonarqube-token-id') // Replace with your SonarQube token ID
        NEXUS_URL = 'http://your-nexus-server'
        NEXUS_REPO = 'your-repo'
        NEXUS_CRED = credentials('nexus-credentials-id') // Replace with your Nexus credentials ID
    }

    stages {
<<<<<<< HEAD
        stage('Checkout') {
            steps {
                // Checkout code from the version control system
                git 'https://github.com/your-repository-url.git'
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
