pipeline {
    agent any      //agent { label 'ec2-slave'}
    tools {
        maven 'M2_HOME'
        //jdk 'JAVA_HOME'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/aaditya7577/simple-java-maven-app.git'
            }
        }
        stage('Maven') {
            steps {
                sh 'mvn package' 
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }
}
