# Lab 7: Docker Volume and Bind Mount with Nginx

## Objective

This lab demonstrates how to use Docker Volumes and Bind Mounts with Nginx. Docker Volumes are used to persist Nginx logs, while Bind Mounts are used to serve custom web content from the host machine.

---

## Step 1: Create a Docker Volume

Create a volume to persist Nginx logs.

```bash
docker volume create nginx_logs
```

Verify the volume.

```bash
docker volume ls
```

Inspect the volume.

```bash
docker volume inspect nginx_logs
```

The default Docker volume path is similar to:

```text
/var/lib/docker/volumes/nginx_logs/_data
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20213717.png?raw=true" width="900">

---

## Step 2: Create a Bind Mount Directory

Create the required directories.

```bash
mkdir -p nginx-bind/html
```

Create the HTML file.

```bash
echo "Hello from Bind Mount" > nginx-bind/html/index.html
```

Verify the file.

```bash
cat nginx-bind/html/index.html
```


## Step 3: Run the Nginx Container

Run the container with both a Docker Volume and a Bind Mount.

```bash
docker run -d \
--name nginx-container \
-p 8080:80 \
-v nginx_logs:/var/log/nginx \
-v $(pwd)/nginx-bind/html:/usr/share/nginx/html \
nginx
```

Verify the container is running.

```bash
docker ps
```


## Step 4: Verify the Nginx Page

```bash
curl http://localhost:8080
```

Expected output:

```text
Hello from Bind Mount
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20213944.png?raw=true" width="900">

---

## Step 5: Modify the HTML File

Update the file on the host machine.

```bash
echo "Docker Bind Mount Updated Successfully!" > nginx-bind/html/index.html
```

Verify again.

```bash
curl http://localhost:8080
```

Expected output:

```text
Docker Bind Mount Updated Successfully!
```

### Output

<img src="https://github.com/mohamedadel29/Devops-ivolve-labs/blob/main/images/Screenshot%202026-07-08%20220511.png?raw=true" width="900">

---

## Step 6: Verify Logs in the Docker Volume

Locate the Docker volume.

```bash
docker volume inspect nginx_logs
```

List the stored logs.

```bash
sudo ls /var/lib/docker/volumes/nginx_logs/_data
```

Expected files:

```text
access.log
error.log
```

## Step 7: Stop and Remove the Container

```bash
docker stop nginx-container
```

```bash
docker rm nginx-container
```

---

## Step 8: Delete the Docker Volume

```bash
docker volume rm nginx_logs
```

Verify removal.

```bash
docker volume ls
```

---

## Verification

- ✅ Docker volume created successfully.
- ✅ Volume mounted to `/var/log/nginx`.
- ✅ Bind mount served the custom HTML page.
- ✅ Changes on the host were reflected immediately inside the container.
- ✅ Nginx logs persisted in the Docker volume.
- ✅ Container removed successfully.
- ✅ Docker volume removed successfully.