# Lab 5: Multi-Stage Docker Build for Java Spring Boot Application

## Objective

This lab demonstrates how to create a multi-stage Docker build for a Spring Boot application. The first stage uses Maven to build the application, while the second stage uses a lightweight Java runtime image to run the generated JAR file.

---

## Prerequisites

- Docker
- Git
- Java 17
- Maven

---

## Step 1: Clone the Repository

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1
```

---

## Step 2: Create Multi-Stage Dockerfile

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

## Step 3: Build the Docker Image

```bash
docker build -t app3 .
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20120440.png?raw=true" width="900">

---

## Step 4: Verify Image Size

```bash
docker images
```

Example:

```text
REPOSITORY   TAG      SIZE
app3         latest   229MB
```

---

## Step 5: Run the Container

```bash
docker run -d --name container3 -p 8080:8080 app3
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20120342.png?raw=true" width="900">

---

## Step 6: Test the Application

```bash
curl http://localhost:8080
```

Expected output:

```text
Hello from Dockerized Spring Boot!
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20120305.png?raw=true" width="900">

---

## Step 7: Stop and Remove the Container

```bash
docker stop container3
docker rm container3
```

---

## Step 8: Remove the Docker Image

```bash
docker rmi app3
```

---

## Verification

- ✅ Multi-stage Docker build completed successfully.
- ✅ Spring Boot application packaged successfully.
- ✅ Optimized Docker image created.
- ✅ Container started successfully.
- ✅ Application accessible on port **8080**.
- ✅ Container removed successfully.
- ✅ Docker image removed successfully.