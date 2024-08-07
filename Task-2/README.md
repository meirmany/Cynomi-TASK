<!--- app-name: Jenkins Agent Dockerfile -->

# Jenkins Agent Dockerfile

## Introduction 

This project provides a Dockerfile for a Jenkins agent that installs Maven and Chrome. 
The original Dockerfile installed Gradle, which has been replaced with Maven as per the requirements. 
The goal is to ensure the built Docker image runs without any errors.

## Setup Instructions

## Prerequisites
- Docker installed on your machine 

## Steps to Build and Run the Docker Image 

- $git clone https://github.com/meirmany/Cynomi-TASK.git
- $cd Cynomi-TASK/Task-2
- $docker build -t my-jenkins-agent-maven .
- $sudo docker run -it --name my-jenkins-agent-container my-jenkins-agent-maven /bin/bash

## Installed Software Verification

1. Check Maven Version
- $mvn -v

2. Check Google Chrome Version:
- $google-chrome --version

3. Check ChromeDriver Version:
- chromedriver --version

## Cleaning Up

When you’re done testing, you can stop and remove the container:

- $docker stop my-jenkins-agent-container
- $docker rm my-jenkins-agent-container

## Additional Features or Improvements

1. Image Size Optimization
- Minimize Layers: Combine RUN statements to reduce the number of layers.
- Use a Slim Base Image: Start with a smaller base image like alpine and install only necessary packages.

2. Security Enhancements
- Run as Non-Root User: Modify the Dockerfile to run the Jenkins agent as a non-root user for improved security.

3. Logging and Monitoring
- Enhanced Logging: Configure the container to provide detailed logs for easier troubleshooting.
- Monitoring Integration: Integrate with monitoring tools like Prometheus or Grafana 
  to keep track of container performance and availability.

