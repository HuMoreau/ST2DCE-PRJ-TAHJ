pipeline {
    agent any
    tools {
        maven 'maven'
        docker 'docker'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Deploy') {
            steps {
                docker.withRegistry('https://registry.hub.docker.com', 'docker_auth') {
                    appImage.push()
                }
            }
        }
    }
}