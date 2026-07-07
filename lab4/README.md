# Lab 5: Multi-Stage Docker Build for Spring Boot Application

## Objective

This lab demonstrates how to optimize a Docker image using a multi-stage build. The application is built using Maven in the first stage and packaged into a lightweight Java runtime image in the second stage.

---

## Prerequisites

- Docker
- Java 17
- Maven
- Git

---

## Step 1: Clone the Repository

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
```

Navigate to the project directory.

```bash
cd Docker-1
```

---

## Step 2: Build the Application

Package the Spring Boot application.

```bash
mvn clean package
```

Verify that the JAR file has been generated.

```bash
ls target/
```

Expected output:

```text
demo-0.0.1-SNAPSHOT.jar
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-07%20162518.png?raw=true" width="900">

---

## Step 3: Create Multi-Stage Dockerfile

Create a `Dockerfile` with the following content.

```dockerfile
# Stage 1 - Build
FROM maven:3.9.8-eclipse-temurin-17 AS builder

WORKDIR /app

COPY . .

RUN mvn clean package

# Stage 2 - Runtime
FROM eclipse-temurin:17-jdk

WORKDIR /app

COPY --from=builder /app/target/demo-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

CMD ["java","-jar","app.jar"]
```

---

## Step 4: Build Docker Image

Build the Docker image.

```bash
sudo docker build -t app3 .
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-07%20163516.png?raw=true" width="900">

---

## Step 5: Verify the Image

List Docker images.

```bash
sudo docker images
```

Example output:

```text
REPOSITORY   TAG      SIZE
app3         latest   229MB
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-07%20163540.png?raw=true" width="900">

---

## Step 6: Run the Container

Run the application.

```bash
sudo docker run -d --name container3 -p 8080:8080 app3
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-07%20163620.png?raw=true" width="900">

---

## Step 7: Test the Application

Verify that the application is running.

```bash
curl http://localhost:8080
```

Expected response:

```text
Hello from Dockerized Spring Boot!
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-07%20163700.png?raw=true" width="900">

---

## Step 8: Stop and Remove the Container

```bash
sudo docker stop container3
```

```bash
sudo docker rm container3
```

---

## Verification

The application was successfully built using a multi-stage Docker build.

- ✅ Application packaged successfully.
- ✅ Multi-stage Docker image built successfully.
- ✅ Final image size reduced to approximately **229 MB**.
- ✅ Container started successfully.
- ✅ Application accessible on **port 8080**.
- ✅ Container removed successfully.
- ✅ Docker image removed successfully.