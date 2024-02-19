pipeline {
    agent any
    tools {
        maven 'Maven 3.2.5'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
    }
}