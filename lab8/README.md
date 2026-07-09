# Lab 8: Custom Docker Network for Microservices

## Objective

This lab demonstrates how to create a custom Docker network and connect multiple containers to enable communication between frontend and backend microservices.

---

## Prerequisites

- Docker
- Git
- Python 3

---

## Step 1: Clone the Repository

```bash
git clone https://github.com/Ibrahim-Adel15/Docker5.git
```

Navigate to the project directory.

```bash
cd Docker5
```

---

## Step 2: Create Dockerfile for Frontend

Create a file named `frontend/Dockerfile`.

```dockerfile
FROM python:3.12

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

EXPOSE 5000

CMD ["python","app.py"]
```

Build the frontend image.

```bash
docker build -t frontend1 ./frontend
```


---

## Step 3: Create Dockerfile for Backend

Create a file named `backend/Dockerfile`.

```dockerfile
FROM python:3.12

WORKDIR /app

COPY . .

RUN pip install flask

EXPOSE 5000

CMD ["python","app.py"]
```

Build the backend image.

```bash
docker build -t backend1 ./backend
```

---

## Step 4: Create a Custom Docker Network

```bash
docker network create ivolve-network
```

Verify the network.

```bash
docker network ls
```

---

## Step 5: Run the Backend Container

```bash
docker run -d \
--name backend \
--network ivolve-network \
backend1
```

---

## Step 6: Run Frontend Container (frontend1)

```bash
docker run -d \
--name frontend1 \
--network ivolve-network \
-p 5000:5000 \
frontend1
```

---

## Step 7: Run Another Frontend Container (frontend2)

Run this container using the default Docker network.

```bash
docker run -d \
--name frontend2 \
-p 5001:5000 \
frontend1
```

Verify running containers.

```bash
docker ps
```
---

## Step 8: Verify Communication

Open the application.

```bash
curl http://localhost:5000
```

Or access it from your browser.

```text
http://localhost:5000
```

Verify connectivity from the frontend container.

```bash
docker exec -it frontend1 sh
```

Inside the container:

```bash
curl http://backend:5000
```

Expected result:

```text
Hello from Backend
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20220525.png?raw=true" width="900">

---

## Step 9: Verify frontend2 Cannot Reach Backend

```bash
docker exec -it frontend2 sh
```

Inside the container:

```bash
curl http://backend:5000
```

Expected result:

```text
Could not resolve host: backend
```

Since **frontend2** is attached to the default bridge network, it cannot resolve the backend container running on the custom network.

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20220554.png?raw=true">

---

## Step 10: Stop and Remove Containers

```bash
docker stop frontend1 frontend2 backend
```

```bash
docker rm frontend1 frontend2 backend
```

---

## Step 11: Delete the Docker Network

```bash
docker network rm ivolve-network
```

Verify removal.

```bash
docker network ls
```

---

## Verification

- ✅ Frontend and backend images built successfully.
- ✅ Custom Docker network created.
- ✅ Backend and frontend1 communicated successfully using the custom network.
- ✅ Frontend2 on the default network could not communicate with the backend.
- ✅ Containers removed successfully.
- ✅ Docker network removed successfully.