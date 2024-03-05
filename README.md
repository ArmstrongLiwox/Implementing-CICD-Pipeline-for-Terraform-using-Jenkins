# Implementing CICD Pipeline for Terraform using Jenkins - *Armstrong*
### ***Introduction to CI/CD and its importance in software development***

## Implementing CI/CD Pipeline for Terraform using Jenkins

Welcome to the comprehensive hands-on project on "Implementing CI/CD Pipeline for Terraform using Jenkins." In today's rapidly evolving IT landscape, efficient and reliable deployment of infrastructure is paramount. Continuous Integration and Continuous Deployment (CI/CD) have emerged as indispensable practices, fostering automation and agility in the software development lifecycle. In this project, we will explore the powerful combination of Terraform, a leading Infrastructure as Code (laC) tool, and Jenkins, a widely-used automation server, to streamline and enhance infrastructure deployment workflows.

Project Overview:
In the journey ahead, we will delve into the intricacies of building a robust CI/CD pipeline specifically tailored for Terraform projects. By automating the building, testing, and deployment of infrastructure changes, these pipelines enhance speed, reliability, and consistency across environments. The use of Infrastructure as Code (laC) with Terraform ensures reproducibility and scalability, while Jenkins facilitates collaborative development, visibility, and continuous integration and deployment as you will see in this project. This approach not only reduces time-to-market but also promotes resource efficiency, cost optimization, and compliance with security standards. Overall, CI/CD pipelines with Terraform and Jenkins empower organizations to adapt quickly to changing business requirements, fostering a culture of automation and continuous improvement in the dynamic landscape of modern software development and operations.


Setting Up the Environment
Let's start the project by setting up a Jenkins server running in a docker container.
We will create a Dockerfile to define the configuration for our Jenkins server. This Dockerfile will include the necessary dependencies and configurations to run Jenkins seamlessly, and also to run terraform cli.
Dockerfile for Jenkins
Jenkins comes with a docker image that can be used out of the box to run a container with all the relevant dependencies for Jenkins. But because we have unique requirement to run terraform, we need to find a way to extend the readily available jenkins image.
The Jenkins official docker image can be found here
Extending this image means we have to write our own dockerfile, and include all the other stuff we need. Lets go through that quickly.
1. Create a directory and name it terraform-with-cicd
2. create a file and name it Dockerfile
3. Add the below content in the dockerfile