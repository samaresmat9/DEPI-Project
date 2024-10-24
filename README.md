# Automated Deployment Pipeline with Jenkins and Docker
## Graduation Project Of DEPI DevOps Track 
## Project Overview
 This project automates the setup and deployment process using the following tools:
1. **Terraform** to create an EC2 instance on AWS.
2. **Ansible** to install Docker and Jenkins on the EC2 instance.
3. **Jenkins** for Continuous Integration/Continuous Deployment (CI/CD) to automate the Dockerization and deployment of a Flask Python application.
## Creating EC2 Instance on AWS using Terraform
1. ### Configure Terraform:
  -  **Create VPC** and define the networking structure (subnets, route tables, security 
    groups, etc..).
  - **Outputs**:
    - Capture the public IP of Ec2.
  - The EC2 instance IP will be in the inventory file for Ansible.
2. ### Installing Docker and Jenkins on EC2 using Ansible
 Ansible will handle the installation of Docker and Jenkins on the EC2 instance.
- **Create Ansible Playbook**:
  - Create playbook to install jenkins and docker on Ec2 Instance.
- **Run Ansible Playbook**:
  - Run the playbook
```bash
ansible-playbook -i inventory.yml playbook.yml
```
3. ### Dockerizing Flask App
- **Create Dockerfile**:
  - Inside your Flask app directory, create Dockerfile:
- **Build and Run Docker Container**:
  - Build the Docker image
```bash
docker build -t flask_app .
```
- Run the container:
```bash
docker run -p 5000:5000 flask_app
```
- **push it to DockerHub**
  - push your image to Docker Hub
    - create a new repository in DockerHub.
    - push the image by ```docker push```.
4. ### Automating CI/CD with Jenkins

- **Create Jenkins Pipeline**:
    - In Jenkins, configure a new pipeline job for the Flask app.
    - Add the following Jenkinsfile in your project repository.
- **Set Up Jenkins Webhook**:
    - Go to your GitHub repository settings.
    - set up a webhook to trigger the Jenkins pipeline when code is pushed or updated.
- **Run the Pipeline**:
    - Jenkins will automatically
      -  detect changes in the repository
      -  build the Docker image
      -  test and deploy the Flask application.
  ### Conclusion
  This setup automates the creation of an EC2 instance, the installation of Docker and Jenkins using Ansible, and the           
  Dockerization and deployment of a Flask app. Jenkins ensures that any updates to the repository
  trigger the CI/CD pipeline, keeping the application deployment automated and up-to-date.
    
