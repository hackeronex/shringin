pipeline {
  agent any 
 stages {      
   
      stage ('NIKTO') {
      steps {
       
        sh 'nikto -h demo.testfire.net > /tmp/nikto-output.txt'     
        
         
       }
    }   
   
    stage ('DAST') {
      steps {
        sshagent(['zap']) {
         sh 'ssh -o  StrictHostKeyChecking=no ubuntu@18.218.230.81 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://demo.testfire.net/" || true'
        }
      }
    }
  }
  }
