pipeline {
    agent { label 'docker-label'}
	
	stages {
        stage('clone') {
            steps {
              checkout scm
            }     
        }
	stage('docker build') {
            steps {
              sh "docker build -t chaitra87/web:3.0 ."
		   sh "docker build -t 129037883405.dkr.ecr.us-east-1.amazonaws.com/dockertutorial:latest ."
            }     
        }
	stage('docker push') {
            steps {
		withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dpassw', usernameVariable: 'duname')]) {
		     sh 'docker login -u "${duname}" -p "${dpassw}"'
		     sh "docker push chaitra87/web:2.0"
   
		}              
            }     
        }
	stage('ecr-push') {
            steps { 
                withCredentials([[
                $class: 'AmazonWebServicesCredentialsBinding',
                credentialsId: "awskeys",
                accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                ]]) {
                      sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 129037883405.dkr.ecr.us-east-1.amazonaws.com'
                      sh "docker push 129037883405.dkr.ecr.us-east-1.amazonaws.com/dockertutorial:latest"
              }
            }     
        }
	}
}
