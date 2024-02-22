def dockerfile = 'Dockerfile.jenkins'
def version = ''
def appImage = ''

pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Maven build') {
            agent none
            steps {
                script {
                    versionNumber = "1.0.${BUILD_NUMBER}"
                    sh 'echo set version number'
                    sh 'mvn versions:set -DnewVersion=${version}'
                    sh 'echo build package'
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        stage('Docker build') {
            steps {
                script{
                    appImage = docker.build("thibaulthen/ST2DCE:${version}",
                            "--build-arg VERSION=${version}",
                            "-f ${dockerfile} ./dockerfiles")
                }
            }
        }
    }
}