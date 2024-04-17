@Library('Jenkins-Shared-Library')_
pipeline {
    agent any
    
    environment {
        dockerHubCredentialsID	    = 'DockerHub'  		    			      // DockerHub credentials ID.
        imageName   		            = 'alikhames/python-app'     			// DockerHub repo/image name.
	      k8sCredentialsID	          = 'kubernetes'	    				     // KubeConfig credentials ID.    
    }
    
    stages {       
       
        stage('Build and Push Docker Image') {
            steps {
                script {
                 	
                 		buildandPushDockerImage("${dockerHubCredentialsID}", "${imageName}")
                      
                }
            }
        }

        stage('Deploy on k8s Cluster') {
            steps {
                script { 
                	
				                  deployOnKubernetes("${k8sCredentialsID}", "${imageName}")
                    	
                }
            }
        }
    }

    post {
        success {
            echo "${JOB_NAME}-${BUILD_NUMBER} pipeline succeeded"
        }
        failure {
            echo "${JOB_NAME}-${BUILD_NUMBER} pipeline failed"
        }
    }
}
