pipeline {
    agent none
    stages {
        stage('Checkout Code') {
            agent  { label 'master' }  // This can be problematic if 'master' label is missing
            steps {
                checkout scm
            }
        }
        stage('Compile') {
            agent { label 'compile' }
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            agent { label 'test' }
            steps {
                sh 'mvn test'
            }
        }
    }
}
