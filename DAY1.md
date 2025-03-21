# Installing Jenkins in Linux and creating a freestyle Nginx project


## Installing JDK 17
```bash
sudo apt install -y openjdk-17-jdk
sudo update-alternatives --config java
```

![Screenshot from 2025-03-20 21-18-02](https://github.com/user-attachments/assets/86242693-f978-48b8-a6a4-af7518950a0e)

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

![Screenshot from 2025-03-20 21-19-53](https://github.com/user-attachments/assets/2a71d9b2-3d59-46a1-9792-7810bd596d3a)


## Starting Jenkins
```bash
sudo systemctl status jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```
 - Copy the password provided in this step

![Screenshot from 2025-03-20 21-20-21](https://github.com/user-attachments/assets/46b5e84a-3b7f-43fb-8b17-b5db0cc4eed8)


## Jenkins Initial Setup
 - Open a browser and go to `localhost:8080` and paste in the password

![Screenshot from 2025-03-20 21-21-29](https://github.com/user-attachments/assets/4f9395d4-9f5e-49f5-a78f-5349a19a86ee)


 - Click on `continue`

![Screenshot from 2025-03-20 21-22-05](https://github.com/user-attachments/assets/14a38605-ab73-43c8-b7bd-9641dee5d89c)


 - Click on `Install Suggested Plugins`

![Screenshot from 2025-03-20 21-17-40](https://github.com/user-attachments/assets/089c8ae2-954d-4634-8cc3-4ddff4635ec7)


 - The plugins will eb installed one by one and you'll be redirected to the next page click `Start Jenkins`

![423567666-ebd355c3-034e-4fe8-af74-d780d15bf8d7](https://github.com/user-attachments/assets/fe5683ad-4f30-4e09-a7c7-816b86b310bb)


 - Fill in your details and create user id and password then click `save and continue`
> [!NOTE]  
> Remember this user id and password. This will overwrite the `Initial Password` generated, and will be required to login everytime you restart Jenkins.

![423810766-0146a230-0951-4671-b88c-6ded7564a01f](https://github.com/user-attachments/assets/9e7397f2-2632-47ef-ab12-6e0222f3ae15)



 - Leave the default Jenkins URL then click `Save and Finish`


## Setting up a Nginx freestyle project in Jenkins
 - In Jenkins home page click on `create a job`

![423572475-90d7c7fb-50ed-4bd3-93f4-5afb45a29734](https://github.com/user-attachments/assets/5091575b-2fa0-4c83-8649-d2cffcc1f438)


 - Enter a project name
 - Select `Freestyle Project`
 - Click `Ok`

![423573105-03d4672d-21e5-467f-9742-035c662784b8](https://github.com/user-attachments/assets/d2f98f42-90dc-4d39-898f-d1bd04c17e48)


 - In the next page scroll down to `Build Steps`
 - Click `Add Build Step`
 - Select `Execute Shell`

![423574015-60f7d6b0-85e9-44eb-a78b-9a94e8d46a94](https://github.com/user-attachments/assets/32226535-ea83-4a53-bcc5-56d414602eb4)


 - Paste in the below code
```bash
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

![423575224-27fd056c-ea7e-4069-9f23-fd7887260f96](https://github.com/user-attachments/assets/7bd78d85-5643-4990-90f2-e7fffe09ca42)


 - Click `Build Now` in the left side panel
   
![423575571-290bb3be-cf50-40e8-b42e-a1cc9e2f2341](https://github.com/user-attachments/assets/bcf19ea9-310e-456c-a20f-0b0fd09d5da9)

 - Your first Nginx project using Jenkins is successfully deployed!
 - Click on the Build in `Builds` and click on the `Console Output` to view the logs
![Screenshot from 2025-03-20 21-37-53](https://github.com/user-attachments/assets/86b125e1-f33c-4587-8c28-d7621bfedd6a)
