


```
# Demo App – DevOps Bootcamp Training (TechWorld with Nana)

This repository is part of the **DevOps Bootcamp** from [TechWorld with Nana](https://www.techworld-with-nana.com/devops-bootcamp).  
It is designed as a hands-on training project to help you learn and practice core DevOps concepts, including Docker, container orchestration, and working with multi-component applications.

---

## 📚 Project Purpose

This demo app provides a simple user profile application to help you:

- Understand how to containerize applications with Docker
- Practice running and connecting multiple services (Node.js, MongoDB, Mongo Express)
- Learn how to use Docker Compose for multi-container orchestration
- Prepare for deploying containerized apps in real-world DevOps scenarios

---

## 🛠️ Tech Stack

- **Frontend:** `index.html` with pure JavaScript and CSS
- **Backend:** Node.js with Express
- **Database:** MongoDB
- **Admin UI:** Mongo Express

All components are Docker-based for easy setup and portability.

---

## 🚀 Getting Started

### Running with Docker

#### 1. Create Docker Network (optional)

```bash
docker network create mongo-network
```

#### 2. Start MongoDB

```bash
docker run -d -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=password \
  --name mongodb --net mongo-network mongo
```

#### 3. Start Mongo Express

```bash
docker run -d -p 8081:8081 \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
  --net mongo-network \
  --name mongo-express \
  -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express
```

> _NOTE: Creating a custom Docker network is optional. You can start both containers in the default network by omitting the `--net` flag._

#### 4. Open Mongo Express in your browser

[http://localhost:8081](http://localhost:8081)

#### 5. Create Database and Collection

- In Mongo Express, create a database named `user-account`
- Create a collection named `users` in that database

#### 6. Start the Node.js Application

```bash
cd app
npm install
node server.js
```

#### 7. Access the Application UI

[http://localhost:3000](http://localhost:3000)

---

### Running with Docker Compose

#### 1. Start MongoDB and Mongo Express

```bash
docker-compose -f docker-compose.yaml up
```

- Access Mongo Express at [http://localhost:8081](http://localhost:8081)

#### 2. In Mongo Express UI

- Create a new database: `user-account`
- Create a new collection: `users` in the `user-account` database

#### 3. Start Node.js Server

```bash
cd app
npm install
node server.js
```

#### 4. Access the Application

[http://localhost:3000](http://localhost:3000)

---

### Building the Docker Image

To build a Docker image from the application:

```bash
docker build -t my-app:1.0 .
```

The dot (`.`) at the end specifies the location of the Dockerfile.

---

## 🎯 Learning Objectives

- Practice containerizing applications and managing multi-container setups
- Gain experience with Docker CLI and Docker Compose
- Prepare for more advanced DevOps topics such as CI/CD and Kubernetes

---

Happy DevOps Learning with Nana! 🚀
```






