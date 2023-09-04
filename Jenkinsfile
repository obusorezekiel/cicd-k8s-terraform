pipeline {
    
    tools {
        maven 'Maven3'
    }

    agent any 

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
                    withDockerRegistry(credentialsId:'b331a19b-8da6-4f64-896d-b9c75c58d1ec', toolName: 'docker')

                    sh 'docker build -t obusorezekiel/testingjava:latest .'
                    sh 'docker push obusorezekiel/testingjava:latest'

                }
            }
        }
    }
}