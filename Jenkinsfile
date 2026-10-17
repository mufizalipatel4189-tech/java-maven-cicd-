pipeline {
    agent any
    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }
    stages {
        stage('Checkout Code') { steps { checkout scm } }
        stage('Check Java and Maven') { steps { bat 'java -version && mvn -version' } }
        stage('Build') { steps { bat 'mvn clean compile' } }
        stage('Unit Test') {
            steps { bat 'mvn test' }
            post { always { junit 'target/surefire-reports/*.xml' } }
        }
        stage('Package') { steps { bat 'mvn package -DskipTests' } }
        stage('Deploy') { steps { echo 'Deploying...' } }
    }
    post { success { echo 'Pipeline completed successfully' } }
}