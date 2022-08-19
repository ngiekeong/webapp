pipeline {
      agent any
  
  
  stages {
    stage ('Git Checkout') {
      steps {
      git 'https://github.com/ddsperera/webapp.git' 
      }
    }
  
    
     stage ('Send Dockerfile to Ansible Server') {
      steps {
        sshagent(['Ansible-server']) {
        sh 'ssh -o StrictHostKeyChecking=no root@172.31.22.30'
        sh 'scp /var/lib/jenkins/workspace/devsecops-pipeline/Dockerfile root@172.31.22.30:/home/ubuntu'
       }
    }
     }
    
       stage ('Build Docker Image') {
        steps {
        sshagent(['Ansible-server']) {
        sh 'ssh -o StrictHostKeyChecking=no root@172.31.22.30 cd /home/ubuntu'
        sh 'ssh -o StrictHostKeyChecking=no root@172.31.22.30 docker image build . -t $JOB_NAME:v1.$BUILD_ID '
       }
    }
     }
    
    stage ('Tag Docker Image') {
        steps {
        sshagent(['Ansible-server']) {
        sh 'ssh -o StrictHostKeyChecking=no root@172.31.22.30 cd /home/ubuntu'
        sh 'ssh -o StrictHostKeyChecking=no root@172.31.22.30 docker image tag -t $JOB_NAME:v1.$BUILD_ID ddsperera/$JOB_NAME:v1.$BUILD_ID'
        sh 'ssh -o StrictHostKeyChecking=no root@172.31.22.30 docker image tag -t $JOB_NAME:v1.$BUILD_ID ddsperera/$JOB_NAME:latest'  
       }
    }
     }
  }
}
