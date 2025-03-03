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

3. Configuring Firewall on Digital Ocean: Following security best practices, configure the firewall's inbound rules. In this case, you only allow inbound SSH access from your machine to the Droplet and access to Jenkins ports. restricting all other unnecessary connections.

4. Select the **Networking** option from the left panel, then choose **Firewall**.

   <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/SettingUpFirewall.png?raw=true" width=800 />

5. Click on **Create Firewall**
  
6. Set the firewall rules for incoming traffic.<br>
   Allow SSH access from your machine by adding an inbound rule that allows traffic from the public IP address of your machine on port 22 and Jenkins ports.

   <img src="" width=800 />
   
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
2. Verify the official Jenkins image on DockerHub.

   [Docker Hub](https://hub.docker.com/r/jenkins/jenkins)

3. Run the Docker container. We must map to ports to the host 8080 and 50000. The first port allows us to access the browser, and the second one allows the Master-workers communication.

   ```bash
     docker run \
    -p 8080:8080 \
    -p 50000:50000 \
    -d \
    -v jenkins_home:/var/jenkins_home \
    jenkins/jenkins:lts
     ```
4. Verify that the container is running and the container ID.

   ```bash
   docker ps
   ```
   
4. Enter the Jenkins container and obtain the Initial Administrator password, which is located at /var/jenkins_home/secrets/initialAdminPassword.

   ```bash
   docker exec -it d4d4ccb59734 bash
   cat /var/jenkins_home/secrets/initialAdminPassword 
   ```
5. Verify the mounted volume on Droplet.

   ```bash
   docker volume inspect jenkins_home
   ```

6. Open a browser and navigate to Jenkins.
   [Jenkins](HTTP://198.199.70.18:8080)
   
7. Initialize Jenkins, entering  the password obtained from the Jenkins container.
      
