#!/usr/bin/env groovy

pipeline {
    agent any
    environment
    {
        VERSION = "${BUILD_NUMBER}"
        PROJECT = 'test-jenkins-container'
        IMAGE = "$PROJECT:$VERSION"
        ECRURL = 'https://464045059055.dkr.ecr.us-east-1.amazonaws.com/test-jenkins-container'
        ECRCRED = 'ecr:us-east-1:demo-ecr-credentials'
    }
    stages{
        stage('GETSCM'){
            steps{
                git 'https://github.com/gkrishna9790/jenkins-sagemaker-container-build.git'
            }
        }
        stage('Image Build'){
            steps{
                script{
                docker.build("$IMAGE")
                }
            }
        }
        stage('Push Image'){
            steps{
                script{
                    docker.withRegistry(ECRURL, ECRCRED)
                    {
                        docker.image(IMAGE).push()
                    }
                }
            }
        }
    }
}