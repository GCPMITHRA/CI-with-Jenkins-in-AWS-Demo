pipeline {
    agent any
	environment {
		
		PROJECT_ID = 'advance-state-261418'
                CLUSTER_NAME = 'sprint6-k8s-cluster'
                LOCATION = 'us-central1-c'
                CREDENTIALS_ID = 'advance-state-261418'	
	}
	
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
                   script {
		     myimage = docker.build("gcr.io/advance-state-261418/gcpmithra/devops:${env.BUILD_ID}") 
                   }
                }
	   }
	   stage("Push Docker Image") {
                steps {
                   script {
			   docker.withRegistry('https://gcr.io', 'advance-state-261418') 
			   { 
                            myimage.push("${env.BUILD_ID}")	
			   }
		   }
		}
	   }
		  
	   
           stage('Deploy to K8s') { 
                steps{
                   echo "Deployment started ..."
		   sh 'ls -ltr'
		   sh 'pwd'
		   sh "sed -i 's/tagversion/${env.BUILD_ID}/g' deployment.yaml"
                   step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
		   echo "Deployment Finished ..."
            }
          }
    }
}
