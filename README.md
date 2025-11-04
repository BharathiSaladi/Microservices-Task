# Microservices-Task

## Overview
This document provides details on testing various services after running the `docker-compose` file. These services include User, Product, and Gateway Services. Each service has its own endpoints for testing purposes.

# Creating Docker files for each service

     FROM node:20-alpine
     WORKDIR /app
     COPY package*.json ./
     RUN npm install 
     COPY . .
     EXPOSE <port-number>
     CMD ["npm", "start"]

  create docker files for each service using above code repectively specifying port-number

  Once the docker files are created. build the services and run them using

    docker build -t <micro-service> .
    docker run -p micro-service

  <img width="602" height="306" alt="image" src="https://github.com/user-attachments/assets/b3c2a246-fce4-45a4-82fc-d785cab987c3" />

  <img width="602" height="286" alt="image" src="https://github.com/user-attachments/assets/53b9eebe-ba5f-4f31-b523-d2021cffc70e" />

  <img width="602" height="286" alt="image" src="https://github.com/user-attachments/assets/ee342e2b-3b65-4d0d-9714-ff90ae9b2f10" />
  
  

# Docker Compose Creation,Build and Test

  Create a docker-compose.yml file using the micro-services created.
  

      version: "3.9"
      services: 
      user-service:
        build: ./user-service
        ports:
        - "3000:3000"
      networks:
        - app-network
  
      product-service:
      build: ./product-service
      ports:
        - "3001:3001"
      networks:
        - app-network
  
      gateway-service:
      build: ./gateway-service
      ports:
        - "3003:3003"
      depends_on:
        - user-service
        - product-service
      networks:
        - app-network

    networks:
      app-network:
      driver: bridge


Run the docker-compose.yml file using below command and check if all the services are started.


    docker-compose up -d
    docker ps

  <img width="602" height="250" alt="image" src="https://github.com/user-attachments/assets/7c86981a-79fd-42ab-8d96-2cf02cf3356d" />

  <img width="1317" height="308" alt="image" src="https://github.com/user-attachments/assets/2899a3f8-fa6f-4a38-82b3-36161d3806a3" />



Once the services are running, use the below endpoints to verify the functionality.


http://localhost:3000/users

http://localhost:3001/products

http://localhost:3003/api/users

http://localhost:3003/api/products


<img width="602" height="359" alt="image" src="https://github.com/user-attachments/assets/52354bc7-543c-4cc4-9be6-c558888f50a6" />


<img width="602" height="419" alt="image" src="https://github.com/user-attachments/assets/1d0bf671-11c8-40c8-a829-9ef8e4d988d5" />


<img width="602" height="242" alt="image" src="https://github.com/user-attachments/assets/1a6dcf07-1385-4c68-b9fc-2420dd37bd6b" />











  




  
  
