# Lab 6: Managing Docker Environment Variables Across Build and Runtime

## Objective

This lab demonstrates how to manage Docker environment variables using three different methods:
- Passing variables directly in the `docker run` command.
- Using an environment file.
- Defining default environment variables inside the Dockerfile.

---

## Prerequisites

- Docker
- Git

---

## Step 1: Clone the Repository

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-3.git
```

Navigate to the project directory.

```bash
cd Docker-3
```

---

## Step 2: Create Dockerfile

Create a `Dockerfile` with the following content.

```dockerfile
FROM python:3.12

WORKDIR /app

COPY . .

RUN pip install flask

ENV APP_MODE=production
ENV APP_REGION=canada-west

EXPOSE 8080

CMD ["python","app.py"]
```

---

## Step 3: Build Docker Image

```bash
docker build -t app4 .
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20120440.png?raw=true" width="900">

---

# Method 1: Environment Variables from docker run

Run the container and pass environment variables directly.

```bash
docker run -d \
--name container1 \
-p 8081:8080 \
-e APP_MODE=development \
-e APP_REGION=us-east \
app4
```

Verify the application.

```bash
curl http://localhost:8081
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20122102.png?raw=true" width="900">

---

# Method 2: Environment Variables Using an Environment File

Create a file named `env.list`.

```text
APP_MODE=staging
APP_REGION=us-west
```

Run the container.

```bash
docker run -d \
--name container2 \
-p 8082:8080 \
--env-file env.list \
app4
```

Verify the application.

```bash
curl http://localhost:8080
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20122356.png?raw=true" width="900">

---

# Method 3: Environment Variables from Dockerfile

The Dockerfile already contains:

```dockerfile
ENV APP_MODE=production
ENV APP_REGION=canada-west
```

Run the container.

```bash
docker run -d \
--name container3 \
-p 8083:8080 \
app4
```

Verify the application.

```bash
curl http://localhost:8080
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20122521.png?raw=true" width="900">


---

## Verification

The application was successfully deployed using three different methods for managing environment variables.

- ✅ Docker image built successfully.
- ✅ Environment variables passed using `docker run`.
- ✅ Environment variables loaded using `env.list`.
- ✅ Default environment variables loaded from the Dockerfile.
- ✅ All containers ran successfully.