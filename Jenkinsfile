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
    }
}