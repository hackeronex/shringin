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
      
      
  
    
  stage ('CODE REVIEW') {
      steps {
       
        sh 'rm -rf DVWA || true'        
        sh 'rm -f g1.txt || true'     
       
        sh 'git clone https://github.com/ethicalhack3r/DVWA.git'
       
        sh 'grep -irnH -f listv1.txt DVWA > g1.txt'
        sh 'perl regex.pl'
         
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
