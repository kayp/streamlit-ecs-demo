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


The structure can aslo be written as follows

|- app/
| |-- Dockerfile
| |-- streamlit_app/
| |-- init.py
| |-- page1.py
| |-- page2.py
| |-- requirements.txt
|-- cloudformation/
| |-- ecs-cluster.yaml
| |-- ecs-service.yaml
|-- .gitignore
|-- README.md



