pipeline {
    environment {
        imageName = "bsjung/hello_jwt"
        registryCredential = 'dockerhub-token'
        dockerImage = ''
    }
    agent any
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('1. Docker Build') {
            steps {
                script {
                    echo "1. Docker Building..."
                    dockerImage = docker.build(imageName)
                }
            }
        }
        stage('2. Dockder Push') {
            steps {
                script {
                    echo "2. Docker Pushing..."
                    docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
                            dockerImage.push("latest")
                    }
                }
            }
        }
        stage('3. K8s Deploy') {
            steps {
                script {
                    echo "3. K8s Deploy..."
                }
            }
        }
    }
}