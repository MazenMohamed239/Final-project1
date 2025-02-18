# Weather-App
This project automates the deployment of a Flask-based weather application using Jenkins, Docker, and Ansible. The setup includes building a Docker image, pushing it to Docker Hub, and deploying it on a remote web server.

![Screenshot (652)](https://github.com/user-attachments/assets/904389be-7f5f-4ea6-b8d2-7691436e72b3)

### Project Structure
```

.
├── Dockerfile         # Defines the containerized application
├── Jenkines.txt       # Jenkins pipeline configuration
├── playbook.yaml      # Ansible playbook for deploying the application
└── README.md          # Project documentation
```

### Setup & Deployment Process
#### 1. Build & Push Docker Image
The Dockerfile defines the containerized application:

  -  Uses ```Python 3.9-slim``` as the base image.
  
  -  Copies application files into the container.
  
  -  Installs dependencies.
  
  -  Exposes port 5000.
  
  -  Runs ``app.py`` inside the container.
  
##### To build and push manually:
  ```
docker build -t MazenMohamed239/weatherapp:1.0 .
docker push MazenMohamed239/weatherapp:1.0
```
  
#### 2. Automating CI/CD with Jenkins
The Jenkins pipeline (Jenkines.txt) automates:

   1. Building the Docker image ``(docker.build).``

   2. Pushing the image to DockerHub ``(docker.push).``

   3. Deploying with Ansible ``(ansiblePlaybook).``

##### Triggers:

- On code changes in the repository.
- Sends email notifications on success or failure.
  
#### 3. Deployment with Ansible
The Ansible playbook ```(playbook.yaml)``` deploys the app:

-  Installs Docker on target servers.

-  Pulls the latest Docker image from DockerHub.

-  Runs the container on port 5000.
##### To run manually
```
  ansible-playbook -i inventory.yaml playbook.yaml
```
##### Prerequisites :
1. Jenkins installed and configured with:

    - Docker and Ansible installed on the Jenkins server.
    - Credentials for DockerHub (dockerhub-credentials).
    - SSH access to target servers (aws-ssh-key).
2. Docker & Ansible installed on target machines.
3. Security Group Rules:
Allow SSH (22), HTTP (80), and port 5000.

#### Usage
1. Trigger the Jenkins pipeline manually or via Git push.

2. Jenkins builds & pushes the Docker image to DockerHub.

3. Ansible deploys the container on the web server.

Access the app:
```
http://your-server-ip:5000
```

### First EC2 Screenshot
![Screenshot (648)](https://github.com/user-attachments/assets/c88986f9-c873-4a60-92e1-312087bf5b11)

### Second EC2 Screenshot
![Screenshot (649)](https://github.com/user-attachments/assets/f963a4cc-8356-46a5-aab0-de0902f8b84e)



