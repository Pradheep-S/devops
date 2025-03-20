# Installing Jenkins in Linux and creating a freestyle Nginx project


## Installing JDK 17
```bash
sudo apt install -y openjdk-17-jdk
sudo update-alternatives --config java
```

![Screenshot from 2025-03-18 16-29-41](https://github.com/user-attachments/assets/0a5caef6-c19a-4671-92f6-e8bd03d6782b)
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

![Screenshot from 2025-03-18 16-30-12](https://github.com/user-attachments/assets/58ecbfff-0560-4f9c-8b09-bf01dc81d1f8)
## Starting Jenkins
```bash
sudo systemctl status jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```
 - Copy the password provided in this step
   
![Screenshot from 2025-03-18 16-30-44](https://github.com/user-attachments/assets/35ac9957-d12c-4f14-8511-bb1398efa5b6)

## Jenkins Initial Setup
 - Open a browser and go to `localhost:8080` and paste in the password
## Setting up a Nginx freestyle project in Jenkins
 - In Jenkins home page click on `create a job`
 - Enter a project name
 - Select `Freestyle Project`
 - Click `Ok`
   
![Screenshot from 2025-03-19 09-02-36](https://github.com/user-attachments/assets/fe697d8a-8be9-4f01-9291-05984d76c54b)

 - In the next page scroll down to `Build Steps`
 - Click `Add Build Step`
 - Select `Execute Shell`
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

 - Click `Build Now` in the left side panel
 - Your first Nginx project using Jenkins is successfully deployed!
 - Click on the Build in `Builds` and click on the `Console Output` to view the logs

![Screenshot from 2025-03-19 09-03-13](https://github.com/user-attachments/assets/354725ed-975d-4059-aa4d-6c3ba9735c37)
