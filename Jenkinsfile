pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/Harikrishna-111/FlaskApp-Deployment-Pipeline-with-Jenkins-and-EC2-py.git'
            }
        }
        stage('Docker Build') {
            steps {
                sh "docker build . --file Dockerfile --tag docker.io/harikrishna111/python-webapp:latest"
            }
            
        }
        stage('Docker Push') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'DockerCred', toolName: 'docker') {
                    sh "make push"  
                        
                    }
                }
            }
            
        }
        stage('Docker Deploy') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'DockerCred', toolName: 'docker') {
                    sh "docker images"  
                    sh "docker run -d -it -p 5000:5000 --name FlaskApp harikrishna111/python-webapp:latest"
                    }
                }
            }
            
        }
    }
}
