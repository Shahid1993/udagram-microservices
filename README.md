# Udagram Image Filtering in Microservice Architecture

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

The project is split into three parts:
1. [The Simple Frontend](/udacity-c3-frontend)
A basic Ionic client web application which consumes the RestAPI Backend. 
2. [The RestAPI Feed Backend](/udacity-c3-restapi-feed), a Node-Express feed microservice.
3. [The RestAPI User Backend](/udacity-c3-restapi-user), a Node-Express user microservice.

## Getting Setup

### Dependencies

#### Cloud Services
- Amazon Web Services - Relational Database Services - PostgreSQL
- Amazon Web Services S3 - Resource hosting and deployments
- Amazon Web Services - IAM account [applicable only if you host your project on the cloud]

#### DevOps Tools:
- Kuberntes
- Docker
- Travis (CI/CD)

#### Frameworks:
- Ionic (Javascript) (Frontend)
- Node.js (Javascript) (Backend)

### Installation

After setting up the dependencies, clone the project and do the following:

#### Build Docker Images

- **Reverse Proxy Image** - `docker build -t {your_docker_hub_username}/reverseproxy /udacity-c3-deployment/docker`
- **Backend User Image** - `docker build -t {your_docker_hub_username}/udacity-restapi-user /udacity-restapi-user`
- **Backend Feed Image** - `docker build -t {your_docker_hub_username}/udacity-restapi-feed /udacity-restapi-feed`
- **Front-end Image** - `docker build -t {your_docker_hub_username}/udacity-frontend /udacity-frontend`


#### Publish Docker Images to DockerHub

- **Reverse Proxy Image** - `docker push {your_docker_hub_username}/reverseproxy`
- **Backend User Image** - `docker push {your_docker_hub_username}/udacity-restapi-user`
- **Backend Feed Image** - `docker push {your_docker_hub_username}/udacity-restapi-feed`
- **Front-end Image** - `docker push {your_docker_hub_username}/udacity-frontend`

#### Deploy Project to a Kubernetes Cluster

- Update the configuration files with your values:
  - `env-configmap.yaml`
  - `aws-secret.yaml`
  - `env-secret.yaml`
- Update deployment files with your dockerHub username:
  - `reverseproxy-deployment.yaml`
  - `backend-user-deployment.yaml`
  - `backend-user-deployment.yaml`
  - `frontend-deployment.yaml`
  - `docker-compose-build.yaml`
  - `docker-compose.yaml`  
- Create deployments
  - `kubectl apply -f backend-user-deployment.yaml`
  - `kubectl apply -f backend-feed-deployment.yaml`
  - `kubectl apply -f backend-reverseproxy-deployment.yaml`
  - `kubectl apply -f backend-frontend-deployment.yaml`
- Run services
  - `kubectl apply -f backend-user-service.yaml`
  - `kubectl apply -f backend-feed-service.yaml`
  - `kubectl apply -f backend-reverseproxy-service.yaml`
  - `kubectl apply -f backend-frontend-service.yaml`

#### Start the app as a container on a local system
  - Inside udacity-c3-deployment/docker/ directory, run `docker-compose up` to start the application as a container on the local system
