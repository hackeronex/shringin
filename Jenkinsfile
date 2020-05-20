pipeline {
  agent any 
 stages {      
   
   stage ('SSL scan') {
      steps {
         sh 'rm -rf /tmp/outputs/sslscan.txt'
         sh 'sslscan --no-fail demo.testfire.net > /tmp/sslscans.txt'
        
      }
    }
   
   stage ('NMAP') {
      steps {
        sh 'rm -rf /tmp/nmap.txt'       
        sh 'docker run --rm uzyexe/nmap -sS -P0 demo.testfire.net > /tmp/nmaps.txt'     
        
         
       }
    }  
   
    stage ('NIKTO') {
      steps {
         sh 'rm -rf /tmp/niktos.txt'
         sh 'nikto -h demo.testfire.net > /tmp/niktos.txt'     
        
      }
    }
   
  stage ('DIRB') {
      steps {
         sh 'rm -rf /tmp/dirbs.txt'
         sh 'dirb http://demo.testfire.net > /tmp/dirbs.txt'     
        
      }
    }   
        
   
    stage ('ZAP') {
      steps {
        sshagent(['zap']) {
          sh 'rm -rf /tmp/zaps.txt'
         sh 'ssh -o  StrictHostKeyChecking=no ubuntu@18.221.180.103 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://demo.testfire.net > /tmp/zaps.txt" || true'
        }
      }
    }
  }
  }
