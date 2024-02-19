pipeline {
    agent any
    tools {
        maven 'maven'
        dockerTool 'docker'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Docker build') {
            steps {
                sh 'sudo systemctl start docker'
                sh 'docker build -t st2dce-prj-tahj:latest .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker tag st2dce-prj-tahj:latest anthonypab/st2dce-prj-tahj:latest'
                sh 'docker image push anthonypab/st2dce-prj-tahj:latest'
            }
        }
    }
}