pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning from Github repo'
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitLab', url: 'https://github.com/abhinallana/assignment_app.git']]])
                echo 'Successfully cloned'
                
            }
        }
        stage('Create and Push Docker image'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'password', usernameVariable: 'username')]) {
                docker build -t abhinallana/assignment_app:2.0.0 .
                docker --version
                docker push abhinallana/assignment_app:2.0.0
                }
            }
        }
    }
}
