pipeline {
    
    tools {
        maven 'Maven3'
    }

    agent any 

    environment {
        registry = "obusorezekiel/testingjava"
        registryCredential = 'docker-cred'
    }

    stages {
        stage('Git Checkout'){
            steps {
                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/obusorezekiel/cicd-k8s-terraform.git']])
            }
        }

        stage('Build Artifact') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Unit Test'){
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build & Push'){
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }

                }
            }
        }
    }
}