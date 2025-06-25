# Multi-Stage Multi-Agent Jenkins Pipeline

## Project Overview
This project demonstrates a Jenkins pipeline that uses multiple stages and multiple agents to build and test different components of an application. The pipeline leverages Docker containers to provide isolated environments for each stage.

## Technology Stack
- **Jenkins**: Automation server for orchestrating the CI/CD pipeline
- **GitHub**: Source code repository hosting
- **Docker**: Containerization for isolated build environments
- **AWS EC2**: Cloud infrastructure hosting the Jenkins server

## Pipeline Structure
The pipeline consists of two distinct stages, each running in its own Docker container:

### 1. Back-end Stage
- **Environment**: Maven with Java 11 (AdoptOpenJDK)
- **Actions**: 
  - Pulls the `maven:3.8.1-adoptopenjdk-11` Docker image if not present
  - Runs Maven commands in an isolated container
  - Verifies Maven and Java versions

### 2. Front-end Stage
- **Environment**: Node.js 16 (Alpine Linux)
- **Actions**:
  - Pulls the `node:16-alpine` Docker image if not present
  - Runs Node.js commands in an isolated container
  - Verifies Node.js version

## Prerequisites
1. Jenkins server installed and configured
2. Docker installed on the Jenkins server
3. Jenkins user added to the docker group
4. GitHub repository with proper webhook configuration
5. AWS EC2 instance with proper security groups

## Pipeline Configuration
The pipeline is defined in a `Jenkinsfile` with the following structure:

```groovy
pipeline {
  agent none
  stages {
    stage('Back-end') {
      agent {
        docker { image 'maven:3.8.1-adoptopenjdk-11' }
      }
      steps {
        sh 'mvn --version'
      }
    }
    stage('Front-end') {
      agent {
        docker { image 'node:16-alpine' }
      }
      steps {
        sh 'node --version'
      }
    }
  }
}
```

## Setup Instructions
1. Install Docker on your Jenkins server
2. Add Jenkins user to the docker group:
   ```bash
   sudo usermod -aG docker jenkins
   sudo systemctl restart jenkins
   ```
3. Create a new Jenkins pipeline job
4. Configure the pipeline to fetch the Jenkinsfile from your GitHub repository
5. Set up GitHub webhooks for automatic triggering

## Expected Output
When the pipeline runs successfully, you should see:
1. Maven version information in the Back-end stage
2. Node.js version information in the Front-end stage
3. Both stages marked as successful in Jenkins
