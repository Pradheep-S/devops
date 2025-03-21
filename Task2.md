# Creating a docker image 
## Installing Docker
  - Enter the following commands to inatall and verify installation of Docker
```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker --now
docker
```
## Download Docker plugins in Jenkins
 - Go to Jenkins `Dashboard` -> `Manage Jenkins` -> `Available Plugins` -> Search `Docker`
 - Select these plugins and Install
    - Docker
    - Docker Commons
    - Docker Pipeline
    - docker-build-step
    - CoudBees Docker Build and Publish
   
![Screenshot from 2025-03-20 10-16-37](https://github.com/user-attachments/assets/65e7f6e0-1279-4c9c-a396-a8c28f595a91)


 - In this page Check the `Restart Jenkins` after installation this will restart Jenkins

![Screenshot from 2025-03-20 10-16-38](https://github.com/user-attachments/assets/0b0c03b2-61a3-45ef-85ae-1fec313684b2)
## Setting up docker credentials
 - Go to Jenkins > `Manage Jenkins` > `Credentials` > `System` > `Global Credentials (Unrestricted)` > `Add Credentials`
 -  Fill your Docker hub `username` , `password`, and in the `id` field enter `docker-seccred`
   
![Screenshot from 2025-03-20 10-18-15](https://github.com/user-attachments/assets/ceb5104e-64e6-4172-beed-5bb2067005a4)
![Screenshot from 2025-03-20 10-18-24](https://github.com/user-attachments/assets/45a2acd4-cd0b-4875-bba9-79faa918a3b6)

## Creating and building a pipeline

 - Go to Jenkins `Dashboard` > `Create a Job`
 - Enter a project name 
 - Select `pipeline`
 - Click `Ok`
   
![Screenshot from 2025-03-20 10-18-52](https://github.com/user-attachments/assets/a36018bb-fd90-4b62-95d7-385d7599b888)

 - Go to `pipeline`
 - Paste this script below and change the credential wherever mentioned:
```groovy
pipeline {
    agent any

    environment {
        IMAGE_NAME = "pradheep255/docker-test"          // Replace with your Docker Hub username and image name
        TAG = "latest"
        CONTAINER_NAME = "my-container"
        PORT = "3001"
    }

    stages {
        
        stage('Clone Repository') {
            steps {
                echo "Cloning GitHub repository..."
                git 'https://github.com/Pradheep-S/docker-test.git'  // Replace with your repo URL
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh 'chmod +x build.sh'
                sh './build.sh'
            }
        }

                stage('Login to Docker Hub') {
            steps {
                echo "Logging into Docker Hub..." // Change the cedentialsID if you have docker credentials already added with another id other than docker-seccred
                withCredentials([usernamePassword(credentialsId: 'docker-seccred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo "Pushing Docker image to Docker Hub..."
                sh "docker tag $IMAGE_NAME:$TAG $IMAGE_NAME:$TAG"
                sh "docker push $IMAGE_NAME:$TAG"
            }
        }

        stage('Deploy Docker Container') {
            steps {
                echo "Deploying Docker container..."
                sh 'chmod +x deploy.sh'
                sh './deploy.sh'
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
        }
        failure {
            echo "Deployment Failed!"
        }
    }
}
```
 - click `save`
 - click `build`

![Screenshot from 2025-03-20 10-22-53](https://github.com/user-attachments/assets/05849642-2099-45b5-aad6-2b1498c10279)
![Screenshot from 2025-03-20 10-19-29](https://github.com/user-attachments/assets/d034f4a7-27a3-434d-b7cc-6855295c6954)
- View `localhost:3001` to see the output
  
![Screenshot from 2025-03-20 10-49-40](https://github.com/user-attachments/assets/499439e7-b19a-4f52-bec8-d687e781fff3)
 - Go to Docker Hub to see your image pushed there
   
![Screenshot from 2025-03-20 10-20-32](https://github.com/user-attachments/assets/5127efb0-1a81-4498-ab77-47a1474d6dc1)
