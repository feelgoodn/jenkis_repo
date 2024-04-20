pipeline { 
    environment {
        IMAGE = "nikhilkothale17/jenkis_cicd"
        registryCredential = 'dockerhub'
        dockerImage = ''
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
                    dockerImage = docker.build "${IMAGE}:latest"
                }
            }
        }

        stage('Push image to docker hub') {
            steps {
                    script {
                        docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                     }
                     }
                }
            }

        stage('run the docker container') {
            steps {
                sh 'docker run -d -p 8000:8342 --name demo-app ${IMAGE}:latest'
            }
        
        } 
    }   
}