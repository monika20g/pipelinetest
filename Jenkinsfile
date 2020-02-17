pipeline {
   agent any
	tools {
    maven 'M2_HOME'
  }	
    stages {

        stage('Pull latest Code') { 
             steps {
              // Get some code from a GitHub repository
              git 'https://github.com/monika20g/pipelinetest.git'
             }
        }
		stage('spinning up docker images'){
        	steps {
                	sh '/usr/local/bin/docker-compose up -d' 
			          }	
        }
     
        stage('Build') { 
            steps {
           
     
        sh "${M2_HOME}/bin/mvn -B  clean package"		
		   
		    
	    }        
        }
        stage('Test') {
            steps {
		    
		echo ${workspace}    
                sh "${M2_HOME}/bin/mvn test"
            }
        }
        stage('Destroy - After Running tests on Containers') { 
            steps {
                sh 'docker stop $(docker ps -a -q)'
                sh 'docker rm $(docker ps -a -q)'
            }
        }
    }
}
