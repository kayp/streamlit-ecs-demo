# streamlit-ecs-demo
# AWS ECS Deployment for Multipage Python Streamlit Application

This repository contains the necessary files and configurations to deploy a multipage Python Streamlit application on AWS ECS (Elastic Container Service).

# AWS ECS Deployment for Multipage Python Streamlit Application

This repository contains the necessary files and configurations to deploy a multipage Python Streamlit application on AWS ECS (Elastic Container Service). 
The project has the following components:

1. Python streamlit app files
2. Cloudformation teamplates for ECS Cluster creation
3. Docker files and instructions to create an ECR repository


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

Streamlit is a python library similar to RShiny in R or D3js in Javascript. It provides the ability to provide a simple front-end with minimal code and is popular among Data Science projects. The demo code used here was obtained from [Streamlit Multipage Demo](https://docs.streamlit.io/get-started/tutorials/create-a-multipage-app) and can be found in the folder [app](./app)

The [Dockerfile](./app/Dockerfile) is used to create the Docket image which is updated to the ECR repo (or DockerHub)

Steps on creating the ECR repo can be found in [ECR Repo Instructions](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html)


### Cloudformation for hosting the service on ECS Cluster

The cloudformation templates to create the ECS cluster and associated services are included in the [cloudformation folder](./cloudformation)


