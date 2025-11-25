# Dockerized Static Web App on AWS

This project demonstrates how to package and deploy a simple static website using Docker and NGINX, and then run it on AWS through an Elastic Beanstalk Docker environment.  
The goal was to gain hands-on experience with containerization, image building, deployment workflows, and troubleshooting across both local and cloud environments.

---

## Overview

The application itself is intentionally simple: a single static HTML page served by NGINX inside a Docker container.

The real value in this project comes from the workflow around it:

- Building a custom Docker image  
- Validating it locally  
- Managing the project with Git and GitHub  
- Deploying it on AWS Elastic Beanstalk  
- Understanding how AWS provisions and runs the environment  

The final result is a fully working public environment running a Docker image built directly from this repository.

---

## Project Structure

```
.
├── Dockerfile      # Defines how the container image is built
└── index.html      # Static web page served by NGINX
```

### Dockerfile  
Uses the official NGINX base image and copies the static website into `/usr/share/nginx/html`, which is NGINX’s default web root.

### index.html  
A minimal HTML page confirming that the container is running correctly.

---

## Local Workflow

The project was first tested locally to validate the Docker image before deploying it to AWS.

### Build the Docker image
```bash
docker build -t mywebapp .
```

### Run the container
```bash
docker run -p 80:80 mywebapp
```

If the browser displays the static page, the local build is successful.

#### Local issue encountered  
Port **80 was already in use** by another container.  
Stopping the previous container resolved the conflict and allowed the new one to run.

---

## Deployment on AWS Elastic Beanstalk

After validating the image locally, it was deployed to Elastic Beanstalk using the Docker platform.

Elastic Beanstalk automatically handled:

- Creating an EC2 instance  
- Building the Docker image from the Dockerfile  
- Launching the container  
- Creating a security group and opening port 80  
- Assigning an Elastic IP  
- Running health checks  
- Setting up logs and monitoring  

Once deployment completed, the environment showed a **green** health status and the static page became publicly accessible.

This step provided practical experience with:

- Instance profiles  
- Service roles  
- Security groups  
- Elastic Beanstalk event logs  
- Understanding how AWS provisions infrastructure around a container  

---

## What I Learned

This project helped me strengthen several practical skills:

- Writing clear Dockerfiles  
- Building and testing Docker images locally  
- Troubleshooting container issues (e.g., port conflicts)  
- Using Git and GitHub for version control  
- Deploying Docker containers using Elastic Beanstalk  
- Understanding Beanstalk health/status messages  
- Seeing the full workflow from local build → container → cloud deployment  

Although the application is simple, the workflow represents a real cloud deployment process: a containerized application packaged locally and launched on fully managed AWS infrastructure.

---





