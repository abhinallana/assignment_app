pipeline {
    agent any
    
    environment {
		DOCKERHUB_CREDENTIALS=credentials('Docker')
	}


    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning from Github repo'
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitLab', url: 'https://github.com/abhinallana/assignment_app.git']]])
                echo 'Successfully cloned'
                
            }
        }
	stage('Login') {
	    steps {
		sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
		    }
		}
        stage('Create and Push Docker image'){
            steps{
                
                sh 'docker --version'
                sh 'docker build -t abhinallana/assignment_app:2.0.0 .'
                sh 'docker push abhinallana/assignment_app:2.0.0'
                
            }
        }
    }
    post {
		always {
			sh 'docker logout'
		}
	}

}
