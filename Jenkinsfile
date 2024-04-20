pipeline {
    environment {
        IMAGE = "nikhilkothale17/jenkis_cicd"
        dockerImage = ''
    }
    agent any
    stages {
        stage('checkout'){
            steps {
                git branch 'main'
                url: 'https://github.com/feelgoodn/jenkis_repo.git'
            }
        }

        stage('Login') {
			steps {
		sh 'echo nikhilkothale17 | docker login -u nikhilkothale17 --password-stdin'
			}
		}
        stage('Build'){
            steps{
                script {
                    dockerImage = docker.build "${IMAGE}:latest"
            }
        }
    }
        stage('Push image to docker hub') {
            steps {
                script {
                    dockerImage.push "${IMAGE}:latest"
                }
            }
        }

        stage('run the docker container') {
            steps {
                sh 'docker run -d -p 8000:8000 --name demp-app ${IMAGE}:latest'
            }
        }
    }
}