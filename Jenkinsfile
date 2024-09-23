pipeline {
    agent none
    stages {
        stage('Checkout Code') {
            agent { node { label 'main' } } // This can be problematic if 'master' label is missing
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
