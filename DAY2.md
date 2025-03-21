![Screenshot from 2025-03-21 01-46-21](https://github.com/user-attachments/assets/a4ac72ec-bf25-439c-9250-c3aae01f188b)![Screenshot from 2025-03-21 01-46-21](https://github.com/user-attachments/assets/05c7c018-eb83-4185-80d3-f4f6183303c7)# Creating a docker image using 
## Installing Docker
  - Enter the following commands to inatall and verify installation of Docker
```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker --now
docker
```
![Screenshot from 2025-03-20 21-43-33](https://github.com/user-attachments/assets/3134fa3c-6a96-4aa5-8210-e7bff7b44301)

## Download Docker plugins in Jenkins
 - Go to Jenkins `Dashboard` -> `Manage Jenkins` -> `Available Plugins` -> Search `Docker`
 - Select these plugins and Install
    - Docker
    - Docker Commons
    - Docker Pipeline
    - docker-build-step
    - CoudBees Docker Build and Publish
![Screenshot from 2025-03-21 01-46-21](https://github.com/user-attachments/assets/84a487ae-ab0c-4d1a-a3fb-2a9991b066d1)
![3](https://github.com/user-attachments/assets/5f43b0b6-19de-46b6-b143-654bacfae677)
![4](https://github.com/user-attachments/assets/51261367-bda9-43a2-9584-a069acba2e70)

 - In this page Check the `Restart Jenkins` after installation this will restart Jenkins

![5](https://github.com/user-attachments/assets/8fa10540-cf47-41fa-9647-ffcfd941bcee)

## Add Jenkins to Docker group
 - Go to terminal and run these commands to add Jenkins to docker group
```bash
sudo usermod - aG docker jenkins
sudo systemctl restart jenkins
sudo reboot
```
- This will do its thing and reboot the system 

## Setting up docker credentials
 - Go to Jenkins > `Manage Jenkins` > `Credentials` > `System` > `Global Credentials (Unrestricted)` > `Add Credentials`
 -  Fill your Docker hub `username` , `password`, and in the `id` field enter `docker-seccred`
## Creating and building a pipeline


 - Go to Jenkins `Dashboard` > `Create a Job`

![7](https://github.com/user-attachments/assets/5b0d6fae-87c9-4444-988c-129d098ada33)

 - Enter a project name 
 - Select `pipeline`
 - Click `Ok`
![8](https://github.com/user-attachments/assets/b52798a2-01c2-49ed-ad4c-490162223187)


 - Go to `pipeline`
 - Paste this script below and change the credential wherever mentioned:
```groovy
pipeline {
    agent any

    environment {
        IMAGE_NAME = "pranesh22/test"          // Replace with your Docker Hub username and image name
        TAG = "latest"
        CONTAINER_NAME = "my-container"
        PORT = "3001"
    }

    stages {
       
        stage('Clone Repository') {
            steps {
                echo "Cloning GitHub repository..."
                git branch:'main', url:'https://github.com/pranesh-22kk/docker_task2.git'  // Replace with your repo URL
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
                echo "Logging into Docker Hub..."
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
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

![9](https://github.com/user-attachments/assets/e9a78e6f-5b5a-4006-bf08-4e36b012c8d0)

 - Go to `localhosy:3001`
   
![Screenshot from 2025-03-20 00-48-06](https://github.com/user-attachments/assets/b0b24a12-c4ca-4fbe-a9c2-87254d92ff33)



