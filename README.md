# streamlit-ecs-demo
# AWS ECS Deployment for Multipage Python Streamlit Application

This repository contains the necessary files and configurations to deploy a multipage Python Streamlit application on AWS ECS (Elastic Container Service).

# AWS ECS Deployment for Multipage Python Streamlit Application

This repository contains the necessary files and configurations to deploy a multipage Python Streamlit application on AWS ECS (Elastic Container Service). 
The project has the following components:

1. Python streamlit app files
2. Cloudformation teamplates for ECS Cluster creation
3. Docker files and instructions to create an ECR repository

## Prerequisites
1. [An AWS account with sufficient permissions](https://aws.amazon.com/resources/create-account/)
2. [Installed Docker engine](https://docs.docker.com/engine/install/)
3. [AWS Command Line Interface (CLI)](https://aws.amazon.com/cli/)
4. [AWS Serverless Application Model (SAM) CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html)


## Directory Structure

The project follows the following directory structure:

```

└───streamlit-ecs-demo
    │   README.md
    │
    ├───app
    │   │   Dockerfile
    │   │   main.py
    │   │   requirements.txt
    │   │
    │   └───pages
    │           1_📈_Plotting_Demo.py
    │           2_🌍_Mapping_Demo.py
    │           3_📊_DataFrame_Demo.py
    │
    └───cloudformation
            cluster.yml
            mp-streamlit.yml
            parent.yml
            vpc.yml


```


### Python Streamlit code

Streamlit is a Python library that simplifies the creation of interactive web applications, similar to RShiny in R or D3.js in JavaScript. It is particularly popular in Data Science projects due to its ease of use and minimal code requirements. The demo code featured in this repository is adapted from the [Streamlit Multipage Demo](https://docs.streamlit.io/get-started/tutorials/create-a-multipage-app) and can be found in the [app](./app) folder.



## Docker Image

The [Dockerfile](./app/Dockerfile) included in the repository is used to build the Docker image. Once built, the image can be pushed to an Elastic Container Registry (ECR) or DockerHub.

### ECR Repository Setup

To set up the ECR repository, follow the steps outlined in the [ECR Repo Instructions](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html). Here is a summary of the steps, assuming the region is `us-east-1`:


```bash
# Create an ECR Repo (e.g., mp-slt)
aws ecr create-repository --repository-name mp-slt

# Obtain login credentials for ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin {YourAccountNumber}.dkr.ecr.us-east-1.amazonaws.com

# Build and tag the Docker image
docker build -t mp-slt .
docker tag mp-slt:latest {YourAccountNumber}.dkr.ecr.us-east-1.amazonaws.com/mp-slt:latest

# Push the Docker image to ECR
docker push {YourAccountNumber}.dkr.ecr.us-east-1.amazonaws.com/mp-slt:latest
```

### Cloudformation for hosting the service on ECS Cluster

The cloudformation templates to create the ECS cluster and associated services are included in the [cloudformation folder](./cloudformation)

1. vpc.yml - Creates VPC
2. cluster.yml - Creates ECS CLuster
3. mp-streamlit.yml - Creates the ECS Service, task, load balancer, target group and related resources to host the Streamlit app container
4. parent.yml - Deploys above stacks usind AWS SAM CLI 

### Deployment of cloudformation stacks
Cloudformation stacks are deployed by [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html)

The following command was used.

```

sam deploy   --template-file parent.yml --stack-name ecs-multipage-streamlit --resolve-s3 --capabilities CAPABILITY_IAM --profile {ProfileName} --region {AWS Region -us-east-1 in this case}

```

### Delete resources

ECR Repo can be deleted from the console. The CLoudformation template console can be used to delete resources for created from SAM CLI. ALternatively, this ccan be accomplished by the following command:

```

sam delete --stack-name ecs-multipage-streamlit  --profile kpaws02 --region us-east-1


```
