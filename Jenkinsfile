pipeline {
    agent any

    environment {
        // FIXED: Using the username that successfully logged in
        DOCKER_USER = "gauravrathod207"
        IMAGE_NAME = "${DOCKER_USER}/hellojava:v1"
    }

    stages {
        stage('Compile') {
            steps {
                sh 'javac HelloWorld.java'
            }
        }

        stage('Run Java') {
            steps {
                sh 'java HelloWorld'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Use double quotes to allow Groovy to interpolate the environment variable
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run Docker Container') {
            steps {
                sh "docker run --rm ${IMAGE_NAME}"
            }
        }

        stage('Docker Hub Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'Docker', // Ensure this ID matches your Jenkins Credentials provider
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push ${IMAGE_NAME}"
            }
        }
    }

    post {
        always {
            // Good practice: Clean up the image from the Jenkins server to save space
            sh "docker rmi ${IMAGE_NAME} || true"
            sh "docker logout"
        }
    }
}
