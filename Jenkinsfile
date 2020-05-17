pipeline {
  agent any 
 stages {      
   
   stage ('Source Composition Analysis') {
      steps {
         sh 'rm owasp* || true'
         sh 'wget "https://raw.githubusercontent.com/cehkunal/webapp/master/owasp-dependency-check.sh" '
         sh 'chmod +x owasp-dependency-check.sh'
         sh 'bash owasp-dependency-check.sh'
         sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
        
      }
    }
   
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
