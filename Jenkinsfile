pipeline { 
    environment {
        IMAGE = "nikhilkothale17/jenkis_cicd"
        dockerImage = ''
        registryCredentials = 'nikhil_dockerhub'
    }
    agent any 
    stages {
        stage('checkout') {
                steps {
                git branch: 'main',
                url: 'https://github.com/feelgoodn/jenkis_repo.git'
                }
        }
        stage('Build') {
            steps {
                script {
                    c = docker.build "${IMAGE}:latest"
                }
            }
        }
       stage('push image to docker hub') {
            steps {
                script{
                    docker.withCredentials(' ', registryCredentials){
                        dockerImage.push()
                    }
                }
            sh 'echo nikhilkothale17 | docker login -u nikhilkothale17 --password-stdin'
        }
    }

        stage('run the docker container') {
            steps {
                sh 'docker run -d -p :8342 --name demo-app ${IMAGE}:latest'
            }
        
        } 
    }   
}