pipeline {
  agent any
    
  tools {nodejs "node6.9.1"}
    
  stages {
        
    stage('Git') {
      steps {
        git 'https://github.com/jfrog-fadir/amazon-clone-with-stripe'
      }
    }
     
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }  
  }
}
