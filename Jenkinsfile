pipeline {
   agent any
    
    stages {
        stage('Checkout GitHub repo') {
            steps {
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Swap-nil-2003/docker-devops-demo.git']])
            }
        }
        stage('Build and Tag Docker Image') {
            steps {
                script {
                    sh 'docker build . -t hellodocker'
                    sh 'docker tag hellodocker swapnilab26/learning'
                }
            }
        }    
        stage('Push the Docker Image to DockerHUb') {
            steps {
                script {
                   withCredentials([string(credentialsId: 'docker01', variable: 'docker_hub')]){
                    sh 'docker login -u swapnilaichbhaumik@gmail.com -p ${docker_hub}'
}
                    sh 'docker push swapnilab26/learning'
                }
            }
        }
        
        stage('Deploy deployment and service file') {
            steps {
                script {
                    kubernetesDeploy configs: 'deploymentsvc.yaml', kubeconfigId: 'k8_auth'
                }
            }
        } 
    }      
}
