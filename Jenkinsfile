
pipeline {
    agent any
    
    environment {
        dockerHubCredentialsID	    = 'DockerHub'  		    			// DockerHub credentials ID.
        imageName   		    = 'engyousry/flaskpythonapp'     			// DockerHub repo/image 

    }
     stages {
        stage('Unit Testing') {
            steps {
                script {
                	// Navigate to the directory contains Dockerfile
                 	dir('app') {
                 		
                                echo "Running Unit testing..."
                                sh "pytest test_app.py "
                    	}
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                	// Navigate to the directory contains Dockerfile
                 	dir('app') {
                 		        echo "Building Docker image..."
                                sh "docker build -t ${imageName}:${BUILD_NUMBER} ."
                    	}
                }
            }
        }
        stage('push Docker Image') {
            steps {
                script {
                	// Navigate to the directory containing Dockerfile
                 	dir('app') {
                                withCredentials([usernamePassword(credentialsId: "${dockerHubCredentialsID}", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                                sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                        }
                        
                        // Build and push Docker image
                        echo "Pushing Docker image..."
                        sh "docker push ${imageName}:${BUILD_NUMBER}"
                    	}
                }
            }
        }


        stage('Deploy on EC2') {
            steps {
                script { 
            		  sh '''
	                        echo "Stopping all active Docker containers..."
	                        docker stop $(docker ps -q) || echo "No active containers to stop."
	                        
	                        echo "Removing all stopped Docker containers..."
	                        docker rm $(docker ps -aq) 
	                    '''	
				    sh "docker run -d -p 5000:5000 ${imageName}:${BUILD_NUMBER}"
                    
                }
            }
        }
    }
post {
    success {
        mail bcc: '', 
            body: 'Jenkins pipeline was a success!', 
            cc: 'mido.aaa27@gmail.com, fatma.elzahraa.ali.75@gmail.com, asmaatarek06@gmail.com', 
            from: '', 
            replyTo: '', 
            subject: 'Depi DevOps Project pipeline succeeded', 
            to: 'Mohammed.yousry510@gmail.com'
        echo "${JOB_NAME}-${BUILD_NUMBER} pipeline succeeded"
    }
    failure {
        mail bcc: '', 
            body: 'Jenkins pipeline failed!', 
            cc: 'mido.aaa27@gmail.com, fatma.elzahraa.ali.75@gmail.com, asmaatarek06@gmail.com', 
            from: '', 
            replyTo: '', 
            subject: 'Depi DevOps Project pipeline failed', 
            to: 'Mohammed.yousry510@gmail.com'
        echo "${JOB_NAME}-${BUILD_NUMBER} pipeline failed"
    }
}
}
