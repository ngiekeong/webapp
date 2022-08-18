pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
     stage ('Send Dockerfile to Ansible Server') {
      steps {
        sshagent(['Ansible-server']) {
        sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.22.30'
        sh 'scp /var/lib/jenkins/workspace/devsecops-pipeline/* ubuntu@172.31.22.30:/home/ubuntu'
       }
    }
    
    
    
  }
}
