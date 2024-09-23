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
                    // Deploy to Tomcat server
                    sh 'scp target/image-filter-app-0.0.1-SNAPSHOT.jar ubuntu@65.2.122.115:/opt/tomcat/webapps/'
                    sh 'ssh ubuntu@65.2.122.115 "sudo systemctl restart tomcat"'
                }
            }
        }
    }
}
