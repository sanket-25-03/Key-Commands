Here’s a detailed breakdown of the Docker commands you listed:

### 1. `docker run <image>`
- This command runs a container from the specified image.
- If the image is not available locally, it will pull the image from Docker Hub.

**Example:**  
```bash
docker run ubuntu
```
- This will start a container using the `ubuntu` image.

---

### 2. `docker pull <image>`
- This command explicitly pulls an image from Docker Hub without running it.

**Example:**  
```bash
docker pull nginx
```
- This will download the `nginx` image.

---

### 3. `docker start <container_id_or_name>`
- Starts an already existing (but stopped) container.

**Example:**  
```bash
docker start my_container
```
- If `my_container` was stopped, this will restart it.

---

### 4. `docker ps`
- Lists running containers.

**Example:**  
```bash
docker ps
```
- Shows container ID, image name, uptime, port mappings, etc.

---

### 5. `docker run -d start`
- This command is incorrect; it likely intends to:
  - `-d`: Run the container in detached mode.
  - `start`: Could be mistaken for a container name or image.

**Corrected Example:**  
```bash
docker run -d ubuntu
```
- Runs an `ubuntu` container in the background.

---

### 6. `docker run -d -p 9000:80 <image>`
- Runs a container in detached mode (`-d`).
- Maps port `9000` on the host to port `80` inside the container.

**Example:**  
```bash
docker run -d -p 9000:80 nginx
```
- Nginx will be accessible at `http://localhost:9000`.

---

### 7. `docker stop <container_id_or_name>`
- Stops a running container.

**Example:**  
```bash
docker stop my_container
```
- Gracefully stops `my_container`.

---

### 8. `docker ps -a`
- Lists **all** containers (running and stopped).

**Example:**  
```bash
docker ps -a
```
- Shows all containers and their states.

---

### 9. `docker run --name <name> -d -p <host_port>:<container_port> <image>`
- `--name <name>`: Assigns a custom name to the container.
- `-d`: Runs in detached mode.
- `-p <host_port>:<container_port>`: Maps ports.

**Example:**  
```bash
docker run --name my_web -d -p 8080:80 nginx
```
- Runs an `nginx` container named `my_web` and maps port `8080` on the host to `80` inside the container.

Let me know if you need further details! 🚀
