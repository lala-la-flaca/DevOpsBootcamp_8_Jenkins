# Installing Jenkins on Digital Ocean  ![jenkins](https://github.com/user-attachments/assets/0a854b64-7e42-4941-af78-bea35ccd2f6f)

## Description

This demo project is part of Module 8: Build Automation & CI/CD with Jenkins from the Nana DevOps Bootcamp. It focuses on setting up **Jenkins** as a **Docker container** on a **DigitalOcean Droplet** for automating builds and deployments.
<br />


## 🚀 Technologies Used

- <b>Docker: Docker for containerization.</b>
- <b>Jenkins: Automation for CI/CD.</b>
- <b>Linux: Ubuntu for Server configuration and management.</b>
- <b>Digital Ocean: Cloud provider for hosting Jenkins server.</b>


## 🎯 Features

- <b>Deploy Jenkins as a Docker Container.</b>
- <b>Persist Data using Docker volumes.</b>
- <b>Initialize Jenkins.</b>


## 🏗 Project Architecture

<img src=""/>


## ⚙️ Project Configuration:

### Creating a Digital Ocean Droplet.

1. Sign up for an account on [DigitalOcean](https://www.digitalocean.com).
2. Create a droplet:<br>
   a) Select **Create Droplet** from the Digital Ocean dashboard. <br>

      <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/create%20a%20droplet%201.png?raw=true" width=800 />
    
   b) Select a region: Select the region closest to your location.<be>

      <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/Droplet%20region.png?raw=true" width=800 />

   c) Select an image: Select the Ubuntu image.<br>

      <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/CreatingDropletChooseImage.png?raw=true" width=800 />
     
     - Choose Size: <br>
       * Droplet type: Select Basic.<br>
       * CPU options: Select Regular SSD and the 24GB option.<br>

   d) Select the SSH key  as the Authentication Method. <br>
    - Generate a New SSH Key (if required): If you do not have an existing SSH key, follow DigitalOceans's guide to create a new pair.
    - Use an existing SSH Key: if you already have a public SSK key pair, navigate to the .ssh folder in your local directory. Copy the public key and paste it into the appropriate field in DigitalOCean's interface.<br>

      <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/DropletSSH.png?raw=true" width=800 />

   e) Select **Create Droplet**

3. Configuring Firewall on Digital Ocean: Following security best practices, configure the firewall's inbound rules. In this case, you only allow inbound SSH access from your machine to the Droplet and access to browser port. restricting all other unnecessary connections.

4. Select the **Networking** option from the left panel, then choose **Firewall**.

   <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/SettingUpFirewall.png?raw=true" width=800 />

5. Click on **Create Firewall**
  
6. Set the firewall rules for incoming traffic.<br>
   Allow SSH access from your machine by adding an inbound rule that allows traffic from the public IP address of your machine on port 22 and browser port.

   
7. SSH into the droplet to verify that everything works as expected.

   ```bash
   ssh root@198.199.70.18
   ```

## Installing Jenkins on Digital Ocean
1. Connect to the droplet and install Docker.

   ```bash
   apt update
   apt install net-tools
   snap install docker
   ```

   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_8_Jenkins/blob/main/Img/3%20Pulling%20and%20Running%20Jenkins%20Container.png" width=800 />

2. Verify the official Jenkins image on DockerHub.

   [Docker Hub](https://hub.docker.com/r/jenkins/jenkins)

3. Run the Docker container while mapping two ports: 8080 and 50000. Port 8080 enables browser access, while port 50000 facilitates communication between the master and worker nodes.

   ```bash
     docker run \
    -p 8080:8080 \
    -p 50000:50000 \
    -d \
    -v jenkins_home:/var/jenkins_home \
    jenkins/jenkins:lts
     ```

   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_8_Jenkins/blob/main/Img/3%20Pulling%20and%20Running%20Jenkins%20Container.png" width=800 />
   
   
4. Verify that the container is running and get its container ID.

   ```bash
   docker ps
   ```

   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_8_Jenkins/blob/main/Img/4%20Jenkins%20container%20running.PNG" width=800 />
   
5. Access the Jenkins container and obtain the Initial Administrator password from: /var/jenkins_home/secrets/initialAdminPassword.

   ```bash
   docker exec -it d4d4ccb59734 bash
   cat /var/jenkins_home/secrets/initialAdminPassword 
   ```

   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_8_Jenkins/blob/main/Img/6%20GEtting%20password%20to%20access%20browser.png" width=800 />
   
6. Verify the volume mounted on the Droplet.

   ```bash
   docker volume inspect jenkins_home
   ```

   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_8_Jenkins/blob/main/Img/7%20Checking%20Mounted%20Volume%20on%20droplet.png" width=800 />

7. Open a browser and go to Jenkins.

   [Jenkins](HTTP://198.199.70.18:8080)
   
8. Initialize Jenkins, entering  the password obtained from the Jenkins container and install suggested plugins.

   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_8_Jenkins/blob/main/Img/8%20Eneter%20passsword%20and%20install%20suggested%20plugins.png" width=800 />
   
9. Jenkins is ready.

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_8_Jenkins/blob/main/Img/9%20Jenkins%20is%20ready.png" width=800 />
   
   
      
