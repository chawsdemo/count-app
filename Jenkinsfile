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
              sh "docker build -t chaitra87/web:2.0 ."
            }     
        }
	tage('docker push') {
            steps {
		withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dpassw', usernameVariable: 'duname')]) {
			sh 'docker login -u "${duname}" -p "${dpassw}"'
			sh "docker push chaitra87/web:2.0"
   
		}              
            }     
        }
	}
}
