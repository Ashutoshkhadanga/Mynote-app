pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/Ashutoshkhadanga/Mynote-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t mynote-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){ 
                    sh "docker tag mynote ashutoshkhadanga/mynote:latest"
                    sh "docker push ashutoshkhadanga/mynote:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
