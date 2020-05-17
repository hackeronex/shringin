pipeline {
  agent any 
 stages {      
   
   stage ('SSL scan') {
      steps {
         sh 'rm -rf /tmp/outputs/sslscan.txt'
         sh 'sslscan --no-fail demo.testfire.net > /tmp/outputs/sslscans.txt'
        
      }
    }
   
   stage ('CODE REVIEW') {
      steps {
       
        sh 'rm -rf DVWA || true'        
        sh 'rm -f g1.txt || true'     
       
        sh 'git clone https://github.com/ethicalhack3r/DVWA.git'
       
        sh 'grep -irnH -f listv1.txt DVWA > g1.txt'
        sh 'perl reg1.pl'
         
       }
    }
   
   
   stage ('NMAP') {
      steps {
        sh 'rm -rf /tmp/outputs/nmap.txt'       
        sh 'docker run --rm uzyexe/nmap -sS -P0 demo.testfire.net > /tmp/outputs/nmaps.txt'     
        
         
       }
    }  
   
   
   stage ('DIRB') {
      steps {
         sh 'rm -rf /tmp/outputs/dirbs.txt'
         sh 'dirb http://demo.testfire.net > /tmp/outputs/dirbs.txt'     
        
      }
    }
   
   stage ('NIKTO') {
      steps {
         sh 'rm -rf /tmp/outputs/niktos.txt'
         sh 'nikto -h demo.testfire.net > /tmp/outputs/niktos.txt'     
        
      }
    }
       
   
    stage ('ZAP') {
      steps {
        sshagent(['zap']) {
          sh 'rm -rf /tmp/outputs/zaps.txt'
         sh 'ssh -o  StrictHostKeyChecking=no ubuntu@18.218.230.81 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://demo.testfire.net > /tmp/outputs/zaps.txt" || true'
        }
      }
    }
  }
  }
