pipeline {
    agent any 	
	
	
    stages {	
	   stage('Checkout Project Code') {            
		steps {
                  checkout scm
		}	
           }
           
	   stage('Build') { 
                steps {
                  echo "Cleaning and packaging..."
                  sh 'mvn clean package'		
                }
           }
	   stage('Test') { 
		steps {
	          echo "Testing..."
		  sh 'mvn test'
		}
	   }
	   stage('Build Docker Image') { 
		steps {
                   echo"Build Image Not Implemented"
                }
	   }
	   stage("Push Docker Image") {
                steps {
                   echo "Push Image Not Implemented"
                }
            }
	   
           stage('Deploy to K8s') { 
                steps{
                   
		   echo "Deployment  Not Implemented"
            }
          }
    }
}
