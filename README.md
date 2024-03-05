# Implementing CICD Pipeline for Terraform using Jenkins - *Armstrong*
### ***Introduction to CI/CD and its importance in software development***

---


Welcome to this comprehensive hands-on project on ***"Implementing CI/CD Pipeline for Terraform using Jenkins."*** 

In today's rapidly evolving IT landscape, efficient and reliable deployment of infrastructure is paramount. 

Continuous Integration and Continuous Deployment (CI/CD) have emerged as indispensable practices, fostering automation and agility in the software development lifecycle. 

In this project, we will explore the powerful combination of Terraform, a leading Infrastructure as Code (laC) tool, and Jenkins, a widely-used automation server, to streamline and enhance infrastructure deployment workflows.

### Project Overview:
In this hands-on project, we will delve into the intricacies of building a robust CI/CD pipeline specifically tailored for Terraform projects. 

By automating the building, testing, and deployment of infrastructure changes, these pipelines enhance speed, reliability, and consistency across environments. 

he use of Infrastructure as Code (laC) with Terraform ensures *reproducibility and scalability*, while Jenkins facilitates *collaborative development, visibility, and continuous integration and deployment*.

This approach not only reduces time-to-market but also promotes resource efficiency, cost optimization, and compliance with security standards. 

Overall, CI/CD pipelines with Terraform and Jenkins empower organizations to adapt quickly to changing business requirements, fostering a culture of automation and continuous improvement in the dynamic landscape of modern software development and operations.

---


### Setting Up the Environment

1. We will start the project by setting up a Jenkins server running in a docker container.

1. We will create a Dockerfile to define the configuration for our Jenkins server. 

This Dockerfile will include the necessary dependencies and configurations to run Jenkins seamlessly, and also to run terraform cli.

### Dockerfile for Jenkins

Jenkins comes with a docker image that can be used out of the box to run a container with all the relevant dependencies for Jenkins. 

But because we have unique requirement to run terraform, we need to find a way to extend the readily available jenkins image.

The Jenkins official docker image can be found here (https://hub.docker.com/_/jenkins/).

Extending this image means we have to write our own dockerfile, and include all the other stuff we need.

 
***Lets go through that quickly***.
1. Create a directory and name it 
```
terraform-with-cicd
```
2. create a file and name it 
```
Dockerfile
```
3. Add the below content in the dockerfile
```
 # Use the official Jenkins base image
 FROM jenkins/jenkins:lts

 # Switch to the root user to install additional packages
 USER root

 # Install necessary tools and dependencies (e.g., Git, unzip, wget, software-properties-common)
 RUN apt-get update && apt-get install -y \
     git \
     unzip \
     wget \
     software-properties-common \
     && rm -rf /var/lib/apt/lists/*

 # Install Terraform
 RUN apt-get update && apt-get install -y gnupg software-properties-common wget \
     && wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg \
     && gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint \
     && echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list \
     && apt-get update && apt-get install -y terraform \
     && rm -rf /var/lib/apt/lists/*

 # Set the working directory
 WORKDIR /app

 # Print Terraform version to verify installation
 RUN terraform --version

 # Switch back to the Jenkins user
 USER jenkins

```
![dockerfile](<images/docker file.jpg>)






















