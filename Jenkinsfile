pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        SONARQUBE_URL = 'http://100.27.230.115:9000'
        SONARQUBE_TOKEN = credentials('sonarqube-token')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Set Permissions') {
            steps {
                sh 'chmod +x gradlew'
            }
        }

        stage('Set Java Version') {
            steps {
                sh 'export JAVA_HOME=/path/to/java17'
                sh 'export PATH=$JAVA_HOME/bin:$PATH'
            }
        }

        stage('Build') {
            steps {
                sh './gradlew clean build --stacktrace --info'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh './gradlew sonarqube -Dsonar.projectKey=my-java-gradle-app -Dsonar.host.url=$SONARQUBE_URL -Dsonar.login=$SONARQUBE_TOKEN --stacktrace --info'
                }
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build("chatla007/my-java-gradle-app:${env.BUILD_ID}")
                }
            }
        }

        stage('Trivy Scan') {
            steps {
                script {
                    sh 'trivy image --exit-code 1 --severity HIGH,CRITICAL chatla007/my-java-gradle-app:${env.BUILD_ID}'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'DOCKERHUB_CREDENTIALS') {
                        dockerImage.push("${env.BUILD_ID}")
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
