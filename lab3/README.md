# Lab 3: Run Java Spring Boot App in a Docker Container

## Objective

This lab demonstrates how to containerize a Java Spring Boot application using Docker, build a Docker image, run a container, and verify that the application is working correctly.

---

## Prerequisites

- Docker Desktop
- Git
- Java 17
- Maven

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

## Step 2: Create the Dockerfile

Create a file named `Dockerfile` with the following content:

```dockerfile
FROM maven:3.9.8-eclipse-temurin-17

WORKDIR /app

COPY . .

RUN mvn package

EXPOSE 8080

CMD ["java","-jar","target/demo-0.0.1-SNAPSHOT.jar"]
```

---

## Step 3: Build the Docker Image

Build the Docker image.

```bash
docker build -t app1 .
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-07%20154939.png?raw=true" width="900">

---

## Step 4: Verify the Image

List available Docker images.

```bash
docker images
```

Example output:

```text
REPOSITORY   TAG      IMAGE ID       SIZE
app1         latest   xxxxxxxxxxxx   867MB
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-07%20155201.png?raw=true" width="900">

---

## Step 5: Run the Container

Run a container named **container1**.

```bash
docker run -d --name container1 -p 8080:8080 app1
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-07%20155347.png?raw=true" width="900">

---

## Step 6: Test the Application

Access the application.

```bash
curl http://localhost:8080
```

Expected response:

```text
Hello from Dockerized Spring Boot!
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-07%20155406.png?raw=true" width="900">

---

## Step 7: Stop and Remove the Container

Stop the running container.

```bash
docker stop container1
```

Remove the container.

```bash
docker rm container1
```

---

## Verification

The application was successfully containerized and tested.

- ✅ Docker image built successfully.
- ✅ Image size verified.
- ✅ Container started successfully.
- ✅ Application accessible on port **8080**.
- ✅ Response received successfully.
- ✅ Container stopped and removed successfully.