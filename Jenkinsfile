pipeline {
    agent docker

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
                sh 'docker build -t abhinallana/assignment_app:2.0.0 .'
                sh 'docker --version'
                sh 'docker push abhinallana/assignment_app:2.0.0'
                }
            }
        }
    }
}
