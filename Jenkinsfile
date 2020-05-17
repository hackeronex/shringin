pipeline {
  agent any 
 stages {      
   
   stage ('SSL scan') {
      steps {
         sh 'rm -rf /tmp/sslscan.txt'
         sh 'sslscan --no-fail demo.testfire.net > /tmp/sslscan.txt'
        
      }
    }
   
   stage ('NMAP') {
      steps {
         sh 'rm -rf /tmp/nmapout.txt'
         sh 'sslscan --no-fail demo.testfire.net > /tmp/nmapout.txt'
        
      }
    }
   stage ('NIKTO') {
      steps {
        sh 'rm -rf /tmp/nikto-output.txt'       
        sh 'docker run --rm uzyexe/nmap -sS -P0 demo.testfire.net > /tmp/nikto-output.txt'     
        
         
       }
    }  
       
   
    stage ('ZAP') {
      steps {
        sshagent(['zap']) {
         sh 'ssh -o  StrictHostKeyChecking=no ubuntu@18.218.230.81 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://demo.testfire.net > /tmp/zap.txt" || true'
        }
      }
    }
  }
  }
