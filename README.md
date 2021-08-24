# Deploying a Flask API

In this project you will containerize and deploy a Flask API to a Kubernetes cluster using Docker, AWS EKS, CodePipeline, and CodeBuild.

## - About the API
The Flask app that will be used for this project consists of a simple API with three endpoints:

- `GET '/'`: This is a simple health check, which returns the response 'Healthy'. 
- `POST '/auth'`: This takes a email and password as json arguments and returns a JWT based on a custom secret.
- `GET '/contents'`: This requires a valid JWT, and returns the un-encrpyted contents of that token. 

The app relies on a secret set as the environment variable `JWT_SECRET` to produce a JWT. The built-in Flask server is adequate for local development, but not production, and thus the production-ready [Gunicorn](https://gunicorn.org/) server is used.

## - About the deployment

### Dependencies
    - Docker Engine
        - Installation instructions for all OSes can be found [here](https://docs.docker.com/install/).
        - For Mac users, if you have no previous Docker Toolbox installation, you can install Docker Desktop for Mac. If you already have a Docker Toolbox installation, please read [this](https://docs.docker.com/docker-for-mac/docker-toolbox/) before installing.
    - AWS account
        - For this work, a AWS account is needed and thus we can deploy the APP to EKS.
     
### Project Steps

    1. Write a Dockerfile for a simple Flask API
    2. Build and test the container locally
    3. Create an EKS cluster
    4. Store a secret using AWS Parameter Store
    5. Create a CodePipeline pipeline triggered by GitHub checkins
    6. Create a CodeBuild stage which will build, test, and deploy your code