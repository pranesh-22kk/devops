# Installing Jenkins in Linux and creating a freestyle Nginx project


## Installing JDK 17
```bash
sudo apt install -y openjdk-17-jdk
sudo update-alternatives --config java
```

![Screenshot from 2025-03-21 01-21-23](https://github.com/user-attachments/assets/a7040eef-2c59-4c6b-8397-2d3f588a0c51)
![Screenshot from 2025-03-17 23-44-53](https://github.com/user-attachments/assets/1c5df5e0-01f4-4eb4-92ff-7be5181db8b4)

## Installing Jenkins
```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

![Screenshot from 2025-03-21 01-22-12](https://github.com/user-attachments/assets/f6ad6b64-20de-4e75-9d86-562221ff24ea)


## Starting Jenkins
```bash
sudo systemctl status jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```
 - Copy the password provided in this step

![Screenshot from 2025-03-21 01-23-16](https://github.com/user-attachments/assets/19f6ace2-f1a4-4420-ba2c-4b1796748cc1)




 - Click on `Install Suggested Plugins`

![Screenshot from 2025-03-21 01-46-21](https://github.com/user-attachments/assets/c6190321-cd74-4962-9661-4d8d729d34f0)


 - The plugins will eb installed one by one and you'll be redirected to the next page click `Start Jenkins`

## Setting up a Nginx freestyle project in Jenkins

Creating a project named nginx_project
![Screenshot from 2025-03-21 01-50-48](https://github.com/user-attachments/assets/2e05a19f-c0b9-43cf-b40b-0ecabf372ecd)


#!/bin/bash
# Update package lists
sudo apt update -y

# Install Nginx
sudo apt install -y nginx

# Start and enable Nginx
sudo systemctl enable nginx.service
sudo systemctl start nginx

# Verify Nginx is running
systemctl status nginx
```

![Screenshot from 2025-03-21 01-20-12](https://github.com/user-attachments/assets/c166fb8e-75a4-4ef3-abe9-bba91775a291)

 - Click `Build Now` in the left side panel

 - Your first Nginx project using Jenkins is successfully deployed!
 - Click on the Build in `Builds` and click on the `Console Output` to view the logs
![Screenshot from 2025-03-21 01-25-04](https://github.com/user-attachments/assets/08a1b7cb-7745-43b7-806c-54c2784642df)

