# Lab 9: Containerized Node.js and MySQL Stack Using Docker Compose

## Objective

This lab demonstrates how to deploy a Node.js application with a MySQL database using Docker Compose. The application uses environment variables to connect to the database, stores MySQL data in a Docker volume, and exposes health and readiness endpoints.

---

## Prerequisites

- Docker
- Docker Compose
- Git

---

## Step 1: Clone the Repository

```bash
git clone https://github.com/Ibrahim-Adel15/kubernets-app.git

cd kubernets-app
```

---

## Step 2: Create Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm","start"]
```

---

## Step 3: Create docker-compose.yml

```yaml
services:
  app:
    build: .
    container_name: node-app
    ports:
      - "3000:3000"
    environment:
      DB_HOST: mysql-db
      DB_USER: root
      DB_PASSWORD: root123
    depends_on:
      - db

  db:
    image: mysql:8.0
    container_name: mysql-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root123
      MYSQL_DATABASE: ivolve
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

---

## Step 4: Build and Run the Application

```bash
docker compose up -d --build
```

### Output

<img src="./images/docker-compose-build.png" width="900">

---

## Step 5: Verify Running Containers

```bash
docker ps
```

Expected containers:

- node-app
- mysql-db

### Output

<img src="./images/docker-ps.png" width="900">

---

## Step 6: Verify the Application

Open the application.

```bash
curl http://localhost:3000
```

### Output

<img src="./images/home-page.png" width="900">

---

## Step 7: Verify Health Endpoint

```bash
curl http://localhost:3000/health
```

Expected Response

```text
iVolve web app is working! Keep calm and code on!
```

### Output

<img src="./images/health.png" width="900">

---

## Step 8: Verify Readiness Endpoint

```bash
curl http://localhost:3000/ready
```

Expected Response

```text
iVolve web app is ready to rock and roll!
```

### Output

<img src="./images/ready.png" width="900">

---

## Step 9: Verify Application Logs

```bash
docker exec -it node-app sh
```

```bash
ls /app/logs
```

Expected output

```text
access.log
```

### Output

<img src="./images/logs.png" width="900">

---

## Step 10: Tag the Docker Image

List available images.

```bash
docker images
```

Tag the application image.

```bash
docker tag kubernets-app-app:latest mohamedadel777/node-app:v1
```

---

## Step 11: Push the Image to Docker Hub

Login.

```bash
docker login
```

Push the image.

```bash
docker push mohamedadel777/node-app:v1
```

### Output

<img src="./images/docker-push.png" width="900">

---

## Verification

- ✅ Node.js application containerized successfully.
- ✅ MySQL database deployed using Docker Compose.
- ✅ Docker Volume created for persistent MySQL storage.
- ✅ Application connected successfully to MySQL.
- ✅ Health endpoint verified.
- ✅ Readiness endpoint verified.
- ✅ Application logs verified.
- ✅ Docker image tagged and pushed to Docker Hub.