pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning from Github repo'
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitLab', url: 'https://github.com/abhinallana/assignment_app.git']]])
                echo 'Successfully cloned'
                sh 'docker --version'
            }
        }
        stage('Create and Push Docker image'){
            agent{
                docker
            
            steps{
                sh 'docker build -t abhinallana/assignment_app:2.0.0 .'
                withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'password', usernameVariable: 'username')]) {
                // some block
                sh 'docker push abhinallana/assignment_app:2.0.0'
                }
            }
          }
        }
    }
}
