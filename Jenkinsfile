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
      
      
    
    
  stage ('Source Composition Analysis') {
      steps {
         sh 'rm owasp* || true'
         sh 'wget "https://raw.githubusercontent.com/cehkunal/webapp/master/owasp-dependency-check.sh" '
         sh 'chmod +x owasp-dependency-check.sh'
         sh 'bash owasp-dependency-check.sh'
         sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
        
      }
    }
    
  stage ('CODE REVIEW') {
      steps {
       
        sh 'rm -rf DVWA'        
        sh 'rm -rf vul.txt'           
        sh 'git clone https://github.com/ethicalhack3r/DVWA.git'
        sh 'wget https://raw.githubusercontent.com/hackeronex/shringin/master/list.txt'
        sh 'grep -irnH -f list DVWA > /tmp/vul.txt'
         
       }
    }
      
       
    
    stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
    
  
    
  
  stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@18.191.104.44:/prod/apache-tomcat-8.5.54/webapps/webapp.war'
              }      
           }       
    }
    
    stage ('DAST') {
      steps {
        sshagent(['zap']) {
         sh 'ssh -o  StrictHostKeyChecking=no ubuntu@3.135.224.151 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://demo.testfire.net/" || true'
        }
      }
    }
  }
  }
