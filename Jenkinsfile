pipeline {
  agent any 
 stages {      
   
   stage ('SSL scan') {
      steps {
         sh 'rm -rf /tmp/sslscan.txt'
         sh 'sslscan --no-fail demo.testfire.net > /tmp/sslscans.txt'
        
      }
    }
   
   
   stage ('NMAP') {
      steps {
        sh 'rm -rf /tmp/nmap.txt'       
        sh 'docker run --rm uzyexe/nmap -sS -P0 demo.testfire.net > /tmp/nmaps.txt'     
        
         
       }
    }  
   
   
   stage ('DIRB') {
      steps {
         sh 'rm -rf /tmp/dirbs.txt'
         sh 'docker run --rm hypnza/dirbuster -u demo.testfire.net > /tmp/dirbs.txt'     
        
      }
    }
   
   stage ('NIKTO') {
      steps {
         sh 'rm -rf /tmp/niktos.txt'
         sh 'nikto -h demo.testfire.net > /tmp/niktos.txt'     
        
      }
    }
       
   
    stage ('ZAP') {
      steps {
        sshagent(['zap']) {
         sh 'ssh -o  StrictHostKeyChecking=no ubuntu@18.218.230.81 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://demo.testfire.net > /tmp/zapstxt" || true'
        }
      }
    }
  }
  }
