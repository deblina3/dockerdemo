pipeline {
 agent 

 stages {
 stage('Checkout GitHub repo') {
 steps {
 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/deblina3/dockerdemo.git']])
 }
 }
 stage('Build and Tag Docker Image') {
 steps {
 script {
 sh 'docker build . -t hellodocker'
 sh 'docker tag hellodocker deblina3/learning'
 }
 }
 }
 stage('Push the Docker Image to DockerHUb') {
    steps {
 script {
 withCredentials([string(credentialsId: 'docker_hub', variable: 'docker_hub')]) {
 sh 'docker login -u deblinachowdhury6@gmail.com -p ${docker_hub}'
 }
 sh 'docker push deblina3/learning'
 }
 }
 }

 stage('Deploy deployment and service file') {
 steps {
 script {
 kubernetesDeploy configs: 'deploymentsvc.yaml', kubeconfigId: 'kb_auth'
 }
 }
 }
 }
 }
