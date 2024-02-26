def version = ''
def appImage = ''
def registryCredentials = 'dockerhub_id'

pipeline {
    agent {
        label 'slave'
    }
    tools {
        maven 'maven'
    }
    stages {
        stage('Maven build') {
            agent none
            steps {
                script {
                    version = "1.0.${BUILD_NUMBER}"
                    sh 'echo set version number'
                    sh "mvn versions:set -DnewVersion=${version}"
                    sh 'echo build package'
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        stage('Docker build') {
            steps {
                script {
                    sh 'echo Build docker image'
                    appImage = docker.build("thibaulthen/st2dce:${version}",
                            "--build-arg VERSION=${version} .")
                }
            }
        }
        stage('Docker push') {
            steps {
                script {
                    sh 'echo push image to docker hub'
                    docker.withRegistry('', registryCredentials) {
                        appImage.push()
                        appImage.push('latest')
                        sh 'echo images successfully pushed'
                    }
                }
            }
        }
    }
}