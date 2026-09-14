pipeline {
    agent any

    environment {
        IMAGE_NAME = "persona-crud"
        SONAR_HOST_URL = "http://sonarqube:9000"
        SONAR_TOKEN = credentials('sonar-token')
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }

    stages {

        stage('Build') {
            agent {
                docker {
                    image 'maven:3.9.6-eclipse-temurin-21'
                    args '-e HOME=/root -u 0'  // run as root for permissions
                }
            }
            steps {
                echo "Building the project with Java 21..."
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Testing') {
            agent {
                docker {
                    image 'maven:3.9.6-eclipse-temurin-21'
                    args '-e HOME=/root -u 0'
                }
            }
            steps {
                echo "Running tests..."
                sh 'mvn test jacoco:report'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('SonarQube') {
            agent {
                docker {
                    image 'maven:3.9.6-eclipse-temurin-21'
                    args '-e HOME=/root -u 0'
                }
            }
            steps {
                echo "Analyzing code with SonarQube..."
                withSonarQubeEnv('SonarQube-Server') {
                    sh """
                        mvn sonar:sonar \
                          -Dsonar.projectKey=persona-crud \
                          -Dsonar.host.url=$SONAR_HOST_URL \
                          -Dsonar.login=$SONAR_TOKEN
                    """
                }
            }
        }

        stage('Build Docker Image') {
            agent any
            steps {
                echo "Building Docker image..."
                sh "docker build -t $IMAGE_NAME:${env.BUILD_NUMBER} ."
            }
        }

        stage('DockerHub') {
            agent any
            steps {
                echo "Pushing image to DockerHub..."
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker tag $IMAGE_NAME:${env.BUILD_NUMBER} $USER/$IMAGE_NAME:${env.BUILD_NUMBER}"
                    sh "docker push $USER/$IMAGE_NAME:${env.BUILD_NUMBER}"
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully. Image published to DockerHub."
        }
        failure {
            echo "The pipeline failed. Check the logs in Jenkins."
        }
    }
}
