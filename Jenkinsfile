pipeline {
    agent none   // Don't run on the master
    stages {
        stage('Checkout Code') {
            agent { label 'master' } // Run this step on the Jenkins master
            steps {
                // Clone the repository from GitHub
                checkout scm
            }
        }
        stage('Compile') {
            agent { label 'compile' }  // Use the 'compile' slave node
            steps {
                // Compile the Maven project
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            agent { label 'test' }  // Use the 'test' slave node
            steps {
                // Run the unit tests
                sh 'mvn test'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
