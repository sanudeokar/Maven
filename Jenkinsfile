pipeline {
    agent none
    stages {
        stage('Compile') {
            agent { label 'slave-compile' }
            steps {
                script {
                    sh 'mvn clean compile'
                }
            }
        }
        stage('Test') {
            agent { label 'slave-test' }
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }
        stage('Package') {
            agent { label 'slave-compile' }
            steps {
                script {
                    sh 'mvn package'
                }
            }
        }
        stage('Deploy') {
            agent { label 'slave-compile' }
            steps {
                script {
                    sh 'scp target/image-filter-app-0.0.1-SNAPSHOT.jar user@your-server:/path/to/deploy'
                    sh 'ssh user@your-server "sudo systemctl restart your-app-service"'
                }
            }
        }
    }
}
