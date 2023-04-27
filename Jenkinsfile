pipeline {
    agent any
    tools{
        maven 'maven 3.9.1'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/IreddyAnilKumar/devops']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t anilimg/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u Ireddyanilkumar -p ${Ireddyanilkumar}'

}
                   sh 'docker push anilimg/devops-integration'
                }
            }
        }
      }
    }

