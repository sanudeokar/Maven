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
    }
}
