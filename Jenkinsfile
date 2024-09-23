pipeline {
    agent {
        node {
            label 'slave-compile' // Ensure this node has Java 17 installed
        }
    }
    tools {
        jdk 'jdk-17' // Name of the JDK configuration as set in Global Tool Configuration
    }
    stages {
        stage('Compile') {
            steps {
                script {
                    sh 'mvn clean compile'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }
        stage('Package') {
            steps {
                script {
                    sh 'mvn package'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Ensure you replace 'user@your-server' and '/path/to/deploy' with your actual details.
                    sh 'scp target/image-filter-app-0.0.1-SNAPSHOT.jar user@your-server:/path/to/deploy'
                    sh 'ssh user@your-server "sudo systemctl restart your-app-service"'
                }
            }
        }
    }
}
