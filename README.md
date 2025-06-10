


```

# Demo App – Deploying Images in Kubernetes from Private Docker Repository  
**DevOps Bootcamp with Nana**

This demo app is designed for hands-on learning in the [DevOps Bootcamp with Nana](https://www.techworld-with-nana.com/devops-bootcamp).  
It demonstrates how to containerize a simple user profile application and deploy it to Kubernetes using images stored in a private Docker registry.

---

## 📚 Overview

This demo app shows a simple user profile app set up using:

- **Frontend:** `index.html` with pure JavaScript and CSS styles
- **Backend:** Node.js with Express module
- **Database:** MongoDB for data storage

All components are Docker-based and can be orchestrated with Docker Compose or deployed to Kubernetes.

---

## 🎯 DevOps & Kubernetes Learning Objectives

- **Containerization:** Build and run multi-component apps with Docker.
- **Private Docker Registry:** Push/pull images securely for production use.
- **Kubernetes Deployment:** Deploy and manage applications in Kubernetes using images from a private registry.
- **DevOps Best Practices:** Practice environment setup, configuration, and automation.

---

## 🏗️ Application Structure

```
project-root/
├── app/               # Node.js backend and static frontend
│   ├── server.js
│   ├── package.json
│   └── public/
│       └── index.html
├── Dockerfile         # For building the app image
├── docker-compose.yaml
└── README.md
```

---

## 🚀 Running the Application

### With Docker

#### To start the application

**Step 1:** Create docker network

```bash
docker network create mongo-network
```

**Step 2:** Start MongoDB

```bash
docker run -d -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=password \
  --name mongodb --net mongo-network mongo
```

**Step 3:** Start mongo-express

```bash
docker run -d -p 8081:8081 \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
  --net mongo-network \
  --name mongo-express \
  -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express
```

> _NOTE: Creating a docker network is optional. You can start both containers in the default network. In this case, just omit the `--net` flag in the `docker run` command._

**Step 4:** Open mongo-express from browser

[http://localhost:8081](http://localhost:8081)

**Step 5:** Create `user-account` database and `users` collection in mongo-express

**Step 6:** Start your Node.js application locally - go to `app` directory of project

```bash
cd app
npm install
node server.js
```

**Step 7:** Access your Node.js application UI from browser

[http://localhost:3000](http://localhost:3000)

---

### With Docker Compose

#### To start the application

**Step 1:** Start MongoDB and mongo-express

```bash
docker-compose -f docker-compose.yaml up
```

_You can access the mongo-express under [http://localhost:8081](http://localhost:8081) from your browser_

**Step 2:** In mongo-express UI - create a new database "user-account"

**Step 3:** In mongo-express UI - create a new collection "users" in the database "user-account"

**Step 4:** Start node server

```bash
cd app
npm install
node server.js
```

**Step 5:** Access the Node.js application from browser

[http://localhost:3000](http://localhost:3000)

---

#### To build a Docker image from the application

```bash
docker build -t my-app:1.0 .
```

The dot (`.`) at the end of the command denotes the location of the Dockerfile.

---

## ☸️ Deploying to Kubernetes from a Private Docker Registry

**As part of the DevOps Bootcamp, you will:**

1. **Build and tag your Docker image.**
2. **Push the image to your private Docker registry (e.g., Docker Hub, GitLab Container Registry, or a self-hosted registry).**
3. **Create a Kubernetes Secret for registry authentication:**

   ```bash
   kubectl create secret docker-registry regcred \
     --docker-server=<your-registry-server> \
     --docker-username=<your-username> \
     --docker-password=<your-password> \
     --docker-email=<your-email>
   ```

4. **Reference the secret in your Kubernetes deployment YAML:**

   ```yaml
   spec:
     containers:
       - name: my-app
         image: <your-private-repo>/my-app:1.0
     imagePullSecrets:
       - name: regcred
   ```

5. **Apply your deployment:**

   ```bash
   kubectl apply -f deployment.yaml
   ```

> _This process ensures your Kubernetes cluster can securely pull images from your private registry._

---

## 📖 Additional Resources

- [DevOps Bootcamp with Nana](https://www.techworld-with-nana.com/devops-bootcamp)
- [Docker Documentation](https://docs.docker.com/)
- [Kubernetes Docs: Pull an Image from a Private Registry](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Node.js Documentation](https://nodejs.org/en/docs/)

---

## 🙌 Contributing

This repository is for demo and learning purposes.  
Feel free to fork, experiment, and submit pull requests as you follow along with the bootcamp!

---

Happy DevOps & Kubernetes Learning! 🚀

```



