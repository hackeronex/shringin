pipeline {
  agent any 
 stages {      
   
   stage ('SSL scan') {
      steps {
         sh 'sslscan --no-fail demo.testfire.net > /tmp/sslscan.txt'
        
      }
    }
   
      stage ('NIKTO') {
      steps {
       
        sh 'nikto -h demo.testfire.net > /tmp/nikto-output.txt'     
        
         
       }
    }   
   
   stage ('NMAP') {
      steps {
       
        sh 'nmap -sS -P0 demo.testfire.net > /tmp/nmap-outt.txt'            
         
       }
    }   
   
    stage ('ZAP') {
      steps {
        sshagent(['zap']) {
         sh 'ssh -o  StrictHostKeyChecking=no ubuntu@18.218.230.81 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://demo.testfire.net/" || true'
        }
      }
    }
  }
  }
