# terraform-prj
terraform based resources creation 

# 📦 Terraform Module: AWS S3 Bucket with Versioning

This Terraform module provisions an AWS S3 bucket with versioning enabled and customizable tags.

## 🚀 Features

- Creates a private S3 bucket
- Enables versioning for object recovery
- Supports environment-based tagging

## 📥 Inputs

| Name         | Description                  | Type   | Required |
|--------------|------------------------------|--------|----------|
| bucket_name  | Name of the S3 bucket         | string | ✅ Yes   |
| environment  | Environment tag (e.g., dev)   | string | ✅ Yes   |

## 📤 Outputs

| Name       | Description             |
|------------|-------------------------|
| bucket_id  | ID of the created bucket |

## 🛠️ Usage

module "my_bucket" {
  source      = "./modules/s3_bucket"
  bucket_name = "chandramohan-devops-logs"
  environment = "dev"
}




=================================================================================================================================================================
=================================================================================================================================================================

## ⚙️ Jenkins Pipeline: Docker Build & Push

Here’s a `README.md` for your Jenkins pipeline repo:

```markdown
# ⚙️ Jenkins Pipeline: Docker Build & Push

This Jenkins pipeline automates the build and deployment of a Docker image to Docker Hub.

## 📋 Pipeline Overview

- **Stage 1**: Checkout source code from Git
- **Stage 2**: Build Docker image
- **Stage 3**: Push image to Docker Hub

## 🧰 Prerequisites

- Jenkins with Docker installed
- Docker Hub credentials stored in Jenkins (`dockerhub-creds`)
- Git repository with a valid `Dockerfile`

## 🧪 Sample Jenkinsfile

```groovy
pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
    IMAGE_NAME = "chandramohan/devops-app"
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/your-username/devops-app.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $IMAGE_NAME .'
      }
    }

    stage('Push to Docker Hub') {
      steps {
        sh '''
          echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
          docker push $IMAGE_NAME
        '''
      }
    }
  }

  post {
    success {
      echo "Docker image pushed successfully!"
    }
    failure {
      echo "Build failed. Check logs."
    }
  }
}
