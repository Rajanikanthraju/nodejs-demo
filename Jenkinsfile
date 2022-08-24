pipeline {
    agent {label 'docker_node'}
    environment {
    dockerhub_login = credentials('dockerhub_login')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/Rajanikanthraju/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t rajanikanthraju/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $dockerhub_login_PSW | docker login -u $dockerhub_login_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push rajanikanthraju/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

