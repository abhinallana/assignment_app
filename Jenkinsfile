pipeline {
    agent {
        docker { image 'node:16.13.1-alpine' }
    }

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
            steps{
                sh 'docker build -t assignment_app .'
                withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'password', usernameVariable: 'username')]) {
                // some block
                sh 'docker push abhinallana/assignment_app:v0'
                }
            }
        }
    }
}
