pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                sh 'javac src/HelloWorld.java'
            }
        }

        stage('Run Java') {
            steps {
                sh 'java -cp src HelloWorld'
            }
        }

       }
       }
