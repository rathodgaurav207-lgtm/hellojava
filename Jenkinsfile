pipeline {
    agent any
 environment {
        IMAGE_NAME = "rathodgaurav207-lgtm/hellojava:v1"
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
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run --rm $IMAGE_NAME'
            }
        }

       }
       }
