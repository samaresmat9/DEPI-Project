# Automated Deployment Pipeline with Jenkins and Docker

## Graduation Project for DEPI DevOps Track

### Project Overview

This project focuses on automating the setup, build, and deployment processes using a combination of the following tools:

1. **Terraform** to provision an EC2 instance on AWS.
2. **Ansible** to install both Docker and Jenkins on the EC2 instance.
3. **Jenkins** to manage Continuous Integration and Continuous Deployment (CI/CD), automating the Dockerization and deployment of a Flask-based Python application.

### Provisioning EC2 Instance with Terraform

1. **Setting Up Terraform**:

   - **VPC Creation**: Define the networking infrastructure (such as subnets, route tables, and security groups).
   - **Outputs**:
     - Capture and display the EC2 instance's public IP address.
     - This IP will be added to the Ansible inventory file for further setup.

2. **Installing Docker and Jenkins on EC2 via Ansible**

   Ansible will be used to automate the installation of Docker and Jenkins on the newly created EC2 instance.

   - **Create an Ansible Playbook**:
     - Write a playbook to handle the installation of Docker and Jenkins on the EC2 instance.
   - **Execute the Playbook**:
     - Run the following command to initiate the setup:
     ```bash
     ansible-playbook -i inventory.yml playbook.yml
     ```

3. **Dockerizing the Flask Application**

   - **Writing the Dockerfile**:
     - Inside the Flask app's directory, create a Dockerfile to define the Docker image.
   - **Build and Run the Docker Container**:
     - Build the Docker image:
     ```bash
     docker build -t flask_app .
     ```
     - Run the Docker container:
     ```bash
     docker run -p 5000:5000 flask_app
     ```
   - **Push to DockerHub**:
     - Create a new repository on DockerHub and push the Docker image:
     ```bash
     docker push <repository_name>
     ```

4. **Automating CI/CD with Jenkins**

   - **Create a Jenkins Pipeline**:
     - Set up a new pipeline job in Jenkins for the Flask application.
     - Add the `Jenkinsfile` to your project repository to define the pipeline steps.
   - **Configuring Webhooks for Automation**:
     - In your GitHub repository, set up a webhook that triggers the Jenkins pipeline when any code changes are pushed or updated.
   - **Pipeline Execution**:
     - Jenkins will automatically:
       - Detect changes in the repository,
       - Build the Docker image,
       - Test the application, and
       - Deploy the Flask app.

### Conclusion

This setup streamlines the deployment process by automating the creation of the EC2 instance, the installation of Docker and Jenkins, and the containerization of the Flask app. With Jenkins integrated into the pipeline, any new changes pushed to the repository will trigger the build, test, and deployment processes, ensuring a smooth and continuous delivery of the application.

