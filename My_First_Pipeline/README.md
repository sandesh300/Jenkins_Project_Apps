# Jenkins Pipeline Project

## Overview
This project demonstrates a simple CI/CD pipeline using Jenkins, Docker, and GitHub. The pipeline runs in a Docker container on an AWS EC2 instance and executes a basic Node.js version check.

## Technical Stack
- **Jenkins**: Automation server for CI/CD
- **GitHub**: Source code repository
- **Docker**: Containerization platform
- **AWS EC2**: Cloud compute instance for hosting Jenkins

## Pipeline Configuration
The pipeline is defined in a `Jenkinsfile` with the following structure:

```groovy
pipeline {
  agent {
    docker { image 'node:16-alpine' }
  }
  stages {
    stage('Test') {
      steps {
        sh 'node --version'
      }
    }
  }
}
```

## Key Components
1. **Docker Integration**:
   - Uses `node:16-alpine` as the build environment
   - Automatically pulls the image if not available locally

2. **Pipeline Stages**:
   - Single test stage that checks the Node.js version
   - Easily extensible for additional build, test, or deploy stages

## Setup Requirements
1. **AWS EC2 Instance**:
   - Ubuntu or Amazon Linux
   - Recommended: t2.medium or larger
   - Security groups allowing HTTP/HTTPS and SSH access

2. **Jenkins Installation**:
   - Latest LTS version
   - Docker plugin installed
   - GitHub integration configured

3. **Docker Configuration**:
   - Docker daemon running
   - Jenkins user added to docker group
   - Proper permissions for `/var/run/docker.sock`

## Implementation Steps
1. Create an EC2 instance with the required specifications
2. Install Jenkins and Docker on the instance
3. Configure Jenkins plugins and system settings
4. Set up the pipeline job pointing to your GitHub repository
5. Run and monitor the pipeline execution

## Expected Output
Successful pipeline execution will show:
- Docker image pull logs
- Node.js version output (v16.20.2 in the example)
- Pipeline status marked as "Success"
