pipeline {
    agent any
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
                def myHome = tool name: 'M2_HOME', type: 'maven'
                sh "${myHome}/bin/mvn -B -DskipTests clean package"

            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
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
