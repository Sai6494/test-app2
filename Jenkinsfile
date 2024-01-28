pipeline {
    agent any
    
    environment {
        dockerImage = ''
        registry = 'saikrishna6494/nodeapp'
        registryCredential = 'DockerHubLogin'
    }
    
    stages {
        stage('Checkout') {  
            steps {
                git url: 'https://github.com/Sai6494/test-app2.git', branch: 'main', credentialsId: 'gitaccess'
            }
        }
        stage('Build Docker image') { 
            steps {
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        stage('Upload Docker Image') {
            steps {    
                script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy app') { 
            steps {
                script {
                    kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "k8scredentials")
                }
            }
        }
    }
}
