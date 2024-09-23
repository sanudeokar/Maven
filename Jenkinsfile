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
                    // Add the Tomcat server's SSH key to known hosts
                    sh 'ssh-keyscan -H 65.2.122.115 >> ~/.ssh/known_hosts'

                    // Use Jenkins credentials for SSH
                    withCredentials([sshUserPrivateKey(credentialsId: 'your-ssh-credentials-id', keyFileVariable: 'SSH_KEY')]) {
                        sh 'scp -i $SSH_KEY target/image-filter-app-0.0.1-SNAPSHOT.jar ubuntu@65.2.122.115:/opt/tomcat/webapps/'
                        sh 'ssh -i $SSH_KEY ubuntu@65.2.122.115 "sudo systemctl restart tomcat"'
                    }
                }
            }
        }
    }
}
