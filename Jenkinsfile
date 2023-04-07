pipeline {
    agent any
    tools {
        maven 'apache-maven-3.8.8'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kapilbadgujar1/kapilproj2']])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t kapilbadgujar/demo-0.0.1-snapshot .'
                }
            }
        }
        stage('Push Docker Image to Docker Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwdidd', variable: 'dockerhubVar')]) {
                    bat 'docker login -u kapilbadgujar -p dckr_pat_L2imqzb-ydGR5rwBtE6a-JdUOSM'
                    }
                    bat 'docker push kapilbadgujar/demo-0.0.1-snapshot'
                }
            }
        }
    }

}
