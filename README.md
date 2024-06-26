## Assignment-1:
```
Create a fork of the following repo (https://github.com/jenkins-docs/simple-node-js-react-npm-app) and add a Jenkins
implementation of fetching the required npm packages to build the website and serve it
locally. The website should be accessible on localhost through the port 3004 and jenkins
server on 3000 with some annotations of the packages used to build the repo and button
to execute the build process.
```
### Solution

#### steps:
  - https://github.com/Buddhadev25/simple-node-js-react-npm-app is created by forking https://github.com/jenkins-docs/simple-node-js-react-npm-app
  - Followed https://www.jenkins.io/doc/book/installing/linux/#debianubuntu to install jenkins in my local machine
  - Firewall Configuration to allow 3000 by running `sudo ufw allow 3000`
  - change Jenkins' default port from 8080 to 3000 on Ubuntu by Modify the Port Setting to `HTTP_PORT=3000` in `/etc/default/jenkins`
  - Install prerequisites node and npm in local machine by executing below commands:
    ```
    sudo apt update
    sudo apt install nodejs
    sudo apt install npm
    ```
  - Modified "start" script in package.json sets the development server port to 3004 when running react-scripts start.
  - Configured http://localhost:3000/job/Assignment-1/ by seting pipeline script from SCM, https://github.com/Buddhadev25/simple-node-js-react-npm-app.git with script path Jenkinsfile

  I've attached screenshots here. 

<p align="center">
  <img src="./Assignment-1/A1.png">
  <img src="./Assignment-1/A2.png">
  <img src="./Assignment-1/Screenshot from 2024-06-23 17-58-21.png">
  <img src="./Assignment-1/Jenkins.png">
  <img src="./Assignment-1/web.png">
  <img src="./Assignment-1/console.png">
</p>

## Assignment-2:

```
In the fork created, create a pipeline to pull the latest postgres, redis and mongo-express and mongo db images and build them as a container locally. The images can be pulled from the public docker registry and hosted in a secured local docker registry (with the same credentials as below). Please connect the mongo-express frontend and mongo db through the following access credentials:

Username: ati
Password: ati1234
```
### Solution

#### steps:
  - Followed https://www.digitalocean.com/community/tutorials/how-to-set-up-a-private-docker-registry-on-ubuntu-18-04 to host a local registry using`registry:2` docker image
  - This Jenkins pipeline script pulls, tags, and pushes Docker images (postgres, redis, mongo, mongo-express) to a locally hosted registry (localhost:5000) with provided credentials, ensuring they are available for deployment or distribution in a CI/CD environment.
  - Configured http://localhost:3000/job/Assignment-2/ by seting pipeline script from SCM, https://github.com/Buddhadev25/simple-node-js-react-npm-app.git with script path Assignment-2/Jenkinsfile
  - Images are stored into /var/lib/registry/docker/registry/v2/repositories in local host
  - Docker Compose configuration defines four services:

    - postgres: Runs PostgreSQL with environment variables set for user, password, and database.
    - redis: Deploys Redis without additional environment configuration.
    - mongodb: Sets up MongoDB with credentials specified
    - mongo-express: Provides a web interface for MongoDB, configured to connect to the MongoDB service with basic authentication using username ati and password ati1234.
  - To start and connect Docker containers ran 'sudo docker-compose up -d'
  - Firewall Configuration to allow 8081 by running `sudo ufw allow 8081`
  - http://0.0.0.0:8081/ is accessible through the mentioned credentials. 

I've attached screenshots here. 

<p align="center">
  <img src="./Assignment-1/Screenshot from 2024-06-23 17-57-50.png">

</p>
