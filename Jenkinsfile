pipeline {
    agent {
        node {
            label 'slave-compile'
        }
    }
    tools {
        jdk 'jdk-17'
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
                    withCredentials([file(credentialsId: 'tomcat-deploy-key', variable: 'SSH_KEY')]) {
                        sh 'scp -i $SSH_KEY target/image-filter-app-0.0.1-SNAPSHOT.jar ubuntu@65.2.122.115:/opt/tomcat/webapps/'
                        sh 'ssh -i $SSH_KEY ubuntu@65.2.122.115 "sudo systemctl restart tomcat"'
                    }
                }
            }
        }
    }
}
