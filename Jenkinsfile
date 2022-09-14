pipeline {
    agent any
    
    tools {dockerTool "docker"}

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning from GitLab repo'
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitLab', url: 'https://gitlab.com/abhinallana/assignment_app.git']]])
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
