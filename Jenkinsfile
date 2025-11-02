pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/seu-usuario/projeto-jenkins-java.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Run') {
            steps {
                bat 'java -jar target/projeto-jenkins-java-1.0-SNAPSHOT.jar'
            }
        }
    }
}
