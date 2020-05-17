pipeline {
  agent any 
 stages {      
   
   stage ('SSL scan') {
      steps {
         sh 'rm -rf /tmp/sslscan.txt'
         sh 'sslscan --no-fail demo.testfire.net > /tmp/sslscan.txt'
        
      }
    }
   
      stage ('NIKTO') {
      steps {
        sh 'rm -rf /tmp/nikto-output.txt'       
        sh 'nikto -h demo.testfire.net > /tmp/nikto-output.txt'     
        
         
       }
    }   
   
    stage ('DAST') {
      steps {
        sshagent(['zap']) {
         sh 'ssh -o  StrictHostKeyChecking=no ubuntu@18.218.230.81 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://demo.testfire.net > /tmp/zap.txt" || true'
        }
      }
    }
  }
  }
