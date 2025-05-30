# Docker Cheat Sheet

A concise, visually organized guide to essential Docker commands for container, image, volume, network, system, and Docker Compose management.

---

## **1. Container Management**

### **`docker run`**
- **Purpose**: Create and start a container from an image
- **Syntax**: `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`
- **Key Options**:
  - `-d` — Run in detached mode (background)
  - `-p` — Map ports (e.g., `-p 8080:80` maps host:container)
  - `--name` — Name the container
  - `-v` — Mount volume (e.g., `-v /host/path:/container/path`)
  - `-e` — Set env variables (e.g., `-e "KEY=value"`)
- **Example**:
  ```bash
  docker run -d -p 8080:80 --name my-nginx nginx
  ```

### **`docker ps`**
- **Purpose**: List running containers
- **Syntax**: `docker ps [OPTIONS]`
- **Key Options**:
  - `-a` — Show all containers (running or stopped)
  - `-q` — Show only container IDs
  - `-l` — Show latest created container
- **Example**:
  ```bash
  docker ps -a
  ```

### **`docker stop`**
- **Purpose**: Stop running containers
- **Syntax**: `docker stop [OPTIONS] CONTAINER [CONTAINER...]`
- **Key Options**:
  - `-t` — Wait time (seconds) before stopping
- **Example**:
  ```bash
  docker stop my-nginx
  ```

### **`docker start`**
- **Purpose**: Start stopped containers
- **Syntax**: `docker start [OPTIONS] CONTAINER [CONTAINER...]`
- **Key Options**:
  - `-i` — Attach STDIN, run interactively
- **Example**:
  ```bash
  docker start my-nginx
  ```

### **`docker rm`**
- **Purpose**: Remove containers
- **Syntax**: `docker rm [OPTIONS] CONTAINER [CONTAINER...]`
- **Key Options**:
  - `-f` — Force remove running container
  - `-v` — Remove associated volumes
- **Example**:
  ```bash
  docker rm -f my-nginx
  ```

---

## **2. Image Management**

### **`docker pull`**
- **Purpose**: Download image from registry
- **Syntax**: `docker pull [OPTIONS] NAME[:TAG]`
- **Key Options**:
  - `--platform` — Set platform (e.g., `linux/amd64`)
- **Example**:
  ```bash
  docker pull nginx:latest
  ```

### **`docker build`**
- **Purpose**: Build image from Dockerfile
- **Syntax**: `docker build [OPTIONS] PATH | URL | -`
- **Key Options**:
  - `-t` — Name and tag (e.g., `name:tag`)
  - `--file, -f` — Path to Dockerfile
  - `--build-arg` — Set build-time variables
- **Example**:
  ```bash
  docker build -t my-app:1.0 .
  ```

### **`docker images`**
- **Purpose**: List local images
- **Syntax**: `docker images [OPTIONS] [REPOSITORY[:TAG]]`
- **Key Options**:
  - `-a` — Show all images (incl. intermediate)
  - `-q` — Show only image IDs
- **Example**:
  ```bash
  docker images
  ```

### **`docker rmi`**
- **Purpose**: Remove images
- **Syntax**: `docker rmi [OPTIONS] IMAGE [IMAGE...]`
- **Key Options**:
  - `-f` — Force removal
- **Example**:
  ```bash
  docker rmi -f nginx
  ```

---

## **3. Volume Management**

### **`docker volume create`**
- **Purpose**: Create a volume
- **Syntax**: `docker volume create [OPTIONS] [VOLUME]`
- **Key Options**:
  - `--driver` — Specify volume driver
- **Example**:
  ```bash
  docker volume create my-volume
  ```

### **`docker volume ls`**
- **Purpose**: List volumes
- **Syntax**: `docker volume ls [OPTIONS]`
- **Key Options**:
  - `-q` — Show only volume names
- **Example**:
  ```bash
  docker volume ls
  ```

### **`docker volume rm`**
- **Purpose**: Remove volumes
- **Syntax**: `docker volume rm [OPTIONS] VOLUME [VOLUME...]`
- **Key Options**:
  - `-f` — Force removal
- **Example**:
  ```bash
  docker volume rm my-volume
  ```

---

## **4. Network Management**

### **`docker network create`**
- **Purpose**: Create a network
- **Syntax**: `docker network create [OPTIONS] NETWORK`
- **Key Options**:
  - `--driver` — Network driver (e.g., `bridge`, `overlay`)
  - `--subnet` — Specify subnet
- **Example**:
  ```bash
  docker network create --driver bridge my-network
  ```

### **`docker network ls`**
- **Purpose**: List networks
- **Syntax**: `docker network ls [OPTIONS]`
- **Key Options**:
  - `-q` — Show only network IDs
- **Example**:
  ```bash
  docker network ls
  ```

### **`docker network connect`**
- **Purpose**: Connect container to network
- **Syntax**: `docker network connect [OPTIONS] NETWORK CONTAINER`
- **Key Options**:
  - `--ip` — Specify IP address
- **Example**:
  ```bash
  docker network connect my-network my-nginx
  ```

---

## **5. System Commands**

### **`docker info`**
- **Purpose**: Show system-wide info
- **Syntax**: `docker info [OPTIONS]`
- **Key Options**:
  - `--format` — Format output with template
- **Example**:
  ```bash
  docker info --format '{{.ServerVersion}}'
  ```

### **`docker version`**
- **Purpose**: Show Docker version
- **Syntax**: `docker version [OPTIONS]`
- **Key Options**:
  - `--format` — Format output with template
- **Example**:
  ```bash
  docker version
  ```

### **`docker system prune`**
- **Purpose**: Remove unused data (containers, networks, images)
- **Syntax**: `docker system prune [OPTIONS]`
- **Key Options**:
  - `-a` — Remove all unused images
  - `-f` — Force removal, no prompt
- **Example**:
  ```bash
  docker system prune -a -f
  ```

---

## **6. Docker Compose**

### **`docker-compose up`**
- **Purpose**: Build, create, start, and attach to service containers
- **Syntax**: `docker-compose up [OPTIONS] [SERVICE...]`
- **Key Options**:
  - `-d` — Run in detached mode
  - `--build` — Build images before starting
- **Example**:
  ```bash
  docker-compose up -d
  ```

### **`docker-compose down`**
- **Purpose**: Stop and remove containers, networks, volumes
- **Syntax**: `docker-compose down [OPTIONS]`
- **Key Options**:
  - `--volumes, -v` — Remove named volumes
- **Example**:
  ```bash
  docker-compose down --volumes
  ```

### **`docker-compose ps`**
- **Purpose**: List containers for Compose project
- **Syntax**: `docker-compose ps [OPTIONS] [SERVICE...]`
- **Key Options**:
  - `-q` — Show only container IDs
- **Example**:
  ```bash
  docker-compose ps
  ```

---
