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
                sh 'docker build -t ST2DCE-PRJ-TAHJ:latest .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker tag ST2DCE-PRJ-TAHJ:1.0 anthonypab/ST2DCE-PRJ-TAHJ:latest'
                sh 'docker image push anthonypab/ST2DCE-PRJ-TAHJ:latest'
            }
        }
    }
}