
![RESYANA CAHYANITA](https://github.com/RevoU-FSSE-2/week-6-resyanac/assets/135514670/49a56bad-f274-4429-b0ed-8fc2d4665501)



# Node.js Dockerization and Docker Hub Deployment Guide

This guide for the process of creating a Docker container for a Node.js application, containing `app.js`, `package.json`, and a `Dockerfile`. Then push this Docker image to  Docker Hub account for easy distribution and deployment.

## Introduction

Hello, Resya here! 23 years old girl in +8 GMT (East Borneo) timezone. I am a Tax Collector and software engineer.

The 6th assignment are Simple node.js project that can be run inside docker container. Therefore, i already succeed to run correctly inside the container. Below explained the guidance.

## Prerequisites

Before you proceed, make sure you have the following installed on your system:

1. Docker: [Download and install Docker](https://www.docker.com/get-started).
2. Check the version on terminal : 
 ```
 docker --version
  ```

 **I have the latest version** 
 
<img width="575" alt="Screen Shot 2023-07-24 at 22 46 15" src="https://github.com/RevoU-FSSE-2/week-6-resyanac/assets/135514670/ed6a70be-302e-44c1-9dc4-4757db06457f">

 
  
## Getting Started

1. **Create the Node.js Application:**
   Create a new folder for Node.js application and place the `app.js` and `package.json` files inside it. The application code should be in `app.js`, and `package.json` should contain the necessary dependencies and scripts.

2. **Write Your Node.js Application (app.js):**
   Write Node.js application logic inside the `app.js` file. This file will be the entry point of this application.

[Download the code](https://gist.github.com/berdoezt/e51718982926f0caa3fcd8ed45111430)

 ```
 const http = require('http');

const hostname = '0.0.0.0';

const port = 3001;

const server = http.createServer((req, res) => {

res.statusCode = 200;

res.setHeader('Content-Type', 'text/plain');

res.end('Hello World');

});

server.listen(port, hostname, () => {

console.log(`Server running at http://${hostname}:${port}/`);

});

   ```


3. **Set Up package.json:**
   Ensure your `package.json` file lists all the dependencies required to run Node.js application. Additionally, define a `"start"` script that will run your application.

```
  npm init -y
   ```

## Dockerizing the Node.js Application

1. **Create a Dockerfile:**
   Create a new file named `Dockerfile` (without any file extensions) in the root directory of Node.js application. The Dockerfile is used to specify the steps required to build the Docker image.

2. **Write the Dockerfile:**
   Inside the `Dockerfile`, add the following content:

   ```Dockerfile
   # Use the official Node.js image as the base image
   FROM node:20

   # Set the working directory inside the container
   WORKDIR /app

   # Copy package.json and package-lock.json (if available)
   COPY package*.json ./

   # Install Node.js dependencies
   RUN npm install

   # Copy the rest of the application code
   COPY . .

   # Expose the port your Node.js app is running on
   EXPOSE 3001

   # Command to start your Node.js application
   CMD ["npm", "app.js"]
   ```

   The above Dockerfile uses the official Node.js image as the base image, installs the dependencies, and sets up the application's working directory.

3. **Build the Docker Image:**
   Open a terminal or command prompt, navigate to your application's root directory (where the `Dockerfile` is located), and run the following command:

   ```
   docker build -t resyanac/nodejs-week-6:0.0.1.RELEASE .
   ```

   The `-t` flag is used to tag the image with a name (`resyanac/nodejs-week-6:0.0.1.RELEASE` in this example). The `.` at the end indicates that the build context is the current directory.

4. **Run the Docker Container:**
   Now that you have built the Docker image, you can run a container from it using the following command:

   ```
   docker run -d -p 3000:3001 resyanac/nodejs-week-6:0.0.1.RELEASE
   ```

   The `-p` flag maps port 3000 of the container to port 3001 of the host system.

   <img width="722" alt="Screen Shot 2023-07-27 at 16 36 43" src="https://github.com/RevoU-FSSE-2/week-6-resyanac/assets/135514670/9940a14f-90fc-4f2a-9a28-569bfea2b655">


6. **Access The Node.js Application:**
   Node.js application should now be accessible at `http://localhost:3000` or `http://0.0.0.0:3001` in web browser.
   
![running](https://github.com/RevoU-FSSE-2/week-6-resyanac/assets/135514670/d92e3ee1-674e-49b8-ae34-24617c98eba1)


![Screen Shot 2023-07-27 at 16 37 06](https://github.com/RevoU-FSSE-2/week-6-resyanac/assets/135514670/e429b4d3-989b-4c6b-8e80-40ca9d2cc02e) ![running 2](https://github.com/RevoU-FSSE-2/week-6-resyanac/assets/135514670/6f19d962-3f9e-47f7-9909-0270c78acfbb)


## Pushing the Docker Image to Docker Hub

1. **Login to Docker Hub:**
Log in to Docker Hub account using the following command:

   ```
   docker login
   ```

   Enter  Docker Hub username and password when prompted.

2. **Push the Docker Image:**
   Now, push the tagged image to Docker Hub:

   ```
   docker push resyanac/nodejs-week-6:0.0.1.RELEASE
   ```

uploaded to my account Docker Hub repository.

## Conclusion

I have successfully dockerized Node.js application and pushed the Docker image to my Docker Hub account. Now, my application can be easily deployed on any system with Docker installed by pulling the image from my Docker Hub repository. This makes it convenient for distribution and ensures consistent deployment across different environments.

![pushed](https://github.com/RevoU-FSSE-2/week-6-resyanac/assets/135514670/5a65a76a-7608-45ee-b159-d2a924769d8e)

