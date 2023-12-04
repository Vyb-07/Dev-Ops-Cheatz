
# Docker Cheatsheet

## Table of Contents

1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Starting Docker Service](#starting-docker-service)
   - [Linux](#linux)
   - [macOS](#macos)
   - [Windows](#windows)
4. [Docker Basics](#docker-basics)
   - [Images](#images)
   - [Containers](#containers)
5. [Dockerfile](#dockerfile)
6. [Docker Compose](#docker-compose)
7. [Networking](#networking)
8. [Volumes](#volumes)
9. [Registry](#registry)
10. [Docker Commands](#docker-commands)
11. [Tips and Tricks](#tips-and-tricks)

## Introduction

Docker is a platform for developing, shipping, and running applications in containers. Containers allow developers to package applications with all the dependencies and ship them as a single package.

## Installation

Visit the [official Docker website](https://docs.docker.com/get-docker/) for detailed instructions on installing Docker on your system.

## Starting Docker Service

### Linux

- **Start Docker Service:**
  ```bash
  sudo service docker start
  ```
  Start the Docker service on Linux systems using systemd.

- **Enable Docker Service (Start on Boot):**
  ```bash
  sudo systemctl enable docker
  ```
  Enable the Docker service to start on boot.

- **Docker Version:**
  ```bash
  docker version
  ```
  Check the installed Docker version.

- **Docker Service Status:**
  ```bash
  sudo service docker status
  ```
  Check the status of the Docker service.

### macOS

- **Start Docker Desktop:**
  - Open Docker Desktop from the Applications folder.
  - Docker Desktop will start automatically.

- **Docker Version:**
  ```bash
  docker version
  ```
  Check the installed Docker version.

- **Docker Service Status:**
  ```bash
  docker info
  ```
  Check the status and information of the Docker service.

### Windows

- **Start Docker Desktop:**
  - Open Docker Desktop from the Start menu.
  - Docker Desktop will start automatically.

- **Docker Version:**
  ```bash
  docker version
  ```
  Check the installed Docker version.

- **Docker Service Status:**
  ```bash
  docker info
  ```
  Check the status and information of the Docker service.

## Docker Basics

### Images

- **Pull an Image:**
  ```bash
  docker pull image_name
  ```
  Pulls a Docker image from a registry, such as Docker Hub.

- **List Images:**
  ```bash
  docker images
  ```
  Displays a list of locally available Docker images.

- **Remove an Image:**
  ```bash
  docker rmi image_name
  ```
  Removes a Docker image from the local machine.

- **Create an Image:**
  ```bash
  docker build -t custom_image_name .
  ```
  Builds a Docker image from a Dockerfile in the current directory.

- **Push Image to Registry:**
  ```bash
  docker push registry/custom_image_name
  ```
  Pushes a Docker image to a registry.

### Containers

- **Run a Container:**
  ```bash
  docker run image_name
  ```
  Creates and starts a container from a specified Docker image.

- **List Running Containers:**
  ```bash
  docker ps
  ```
  Shows a list of running containers.

- **List All Containers (including stopped):**
  ```bash
  docker ps -a
  ```
  Displays all containers, including those that are stopped.

- **Stop a Running Container:**
  ```bash
  docker stop container_id
  ```
  Stops a running container gracefully.

- **Remove a Container:**
  ```bash
  docker rm container_id
  ```
  Removes a stopped container.

- **Container Shell Access:**
  ```bash
  docker exec -it container_id /bin/bash
  ```
  Provides interactive shell access to a running container.

- **Container Stats:**
  ```bash
  docker stats container_id
  ```
  Displays a live stream of container resource usage statistics.

- **Attach to a Running Container:**
  ```bash
  docker attach container_id
  ```
  Attaches the terminal to a running container.

- **Copy files to/from Container:**
  ```bash
  docker cp local_path container_id:/container_path
  ```
  Copies files between the local machine and a container.

- **Inspect Container:**
  ```bash
  docker inspect container_id
  ```
  Shows detailed information about a container.

## Dockerfile

A Dockerfile is a script used to create a Docker image. It contains a set of instructions for building an image.

**Sample Dockerfile:**

```Dockerfile
# Use an official base image
FROM ubuntu:20.04

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container
COPY . .

# Install dependencies
RUN apt-get update && \
    apt-get install -y python3

# Specify the command to run on container start
CMD ["python3", "app.py"]
```

- **FROM:** Specifies the base image.
- **WORKDIR:** Sets the working directory inside the container.
- **COPY:** Copies files from the host to the container.
- **RUN:** Executes commands during the image build process.
- **CMD:** Specifies the default command to run when the container starts.




### Step-by-Step Guide: Using Dockerfile to Create a Docker Image

#### 1. **Create a Dockerfile:**
   Start by creating a text file named `Dockerfile` (without any file extension) in your project directory.

   ```Dockerfile
   # Use an official base image
   FROM ubuntu:20.04

   # Set the working directory inside the container
   WORKDIR /app

   # Copy the current directory contents into the container
   COPY . .

   # Install dependencies (example: installing Python)
   RUN apt-get update && \
       apt-get install -y python3

   # Specify the command to run on container start
   CMD ["python3", "app.py"]
   ```

   This simple example uses an official Ubuntu 20.04 base image, sets the working directory, copies the contents of the current directory into the container, installs Python, and specifies the default command to run when the container starts.

#### 2. **Build the Docker Image:**
   Open a terminal in the directory containing the Dockerfile and run the following command to build the Docker image. Replace `custom_image_name` with the desired name for your image.

   ```bash
   docker build -t custom_image_name .
   ```

   The `-t` flag allows you to tag the image with a name.

#### 3. **Verify Image Creation:**
   After the build process completes, you can verify that the image has been created by running:

   ```bash
   docker images
   ```

   You should see your newly created image in the list.

#### 4. **Run a Container from the Image:**
   Now, you can run a container using the image you just created. Replace `custom_image_name` with the name you used during the build process.

   ```bash
   docker run -it custom_image_name
   ```

   The `-it` flags allow you to interact with the container using an interactive shell.

#### 5. **Explore and Test:**
   Inside the running container, you can explore and test your application or services. Any changes made within the container won't affect the original image unless you explicitly commit those changes.

#### 6. **Exit the Container:**
   When you're done, you can exit the container by typing `exit` in the terminal.

#### 7. **Cleanup (Optional):**
   If you want to remove the container after exiting, you can run the following command:

   ```bash
   docker rm container_id
   ```

   Replace `container_id` with the actual container ID or name.

### Additional Tips:

- You can customize the Dockerfile based on the specific requirements of your application.
- Docker caches each step during the build process. If you make changes to your code and want to rebuild the image, Docker will only rebuild the steps after the one that was modified.



## Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications using YAML files.

**docker-compose.yml**

```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
  app:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "5000:5000"
    volumes:
      - .:/app
    depends_on:
      - database
  database:
    image: postgres:latest
    environment:
      POSTGRES_DB: mydatabase
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
  ```

- **version:** Specifies the Docker Compose file version.
- **services:** Defines the services (containers) to be created.
  - **web:** Example service using an existing image (Nginx).
  - **app:** Example service using a custom Dockerfile.
  - **database:** Example service using an existing image (PostgreSQL).
    - **environment:** Sets environment variables for the database.

### Docker Compose Commands

- **Start Containers:**
  ```bash
  docker-compose up
  ```
  Creates and starts containers as defined in the docker-compose.yml file.

- **Stop and Remove Containers:**
  ```bash
  docker-compose down
  ```
  Stops and removes containers defined in the docker-compose.yml file.

- **Build and Start Containers:**
  ```bash
  docker-compose up --build
  ```
  Builds and starts containers, useful when changes are made

 to Dockerfiles.

- **View Logs:**
  ```bash
  docker-compose logs
  ```
  Displays the logs of all services.

- **List Containers:**
  ```bash
  docker-compose ps
  ```
  Lists containers defined in the docker-compose.yml file.

- **Scale Services:**
  ```bash
  docker-compose up --scale service_name=3
  ```
  Scales the number of containers for a specific service.

## Networking

- **List Networks:**
  ```bash
  docker network ls
  ```
  Lists all Docker networks.

- **Create a Network:**
  ```bash
  docker network create network_name
  ```
  Creates a user-defined Docker network.

- **Inspect Network:**
  ```bash
  docker network inspect network_id
  ```
  Displays detailed information about a Docker network.

## Volumes

- **List Volumes:**
  ```bash
  docker volume ls
  ```
  Lists all Docker volumes.

- **Create a Volume:**
  ```bash
  docker volume create volume_name
  ```
  Creates a named volume.

- **Inspect Volume:**
  ```bash
  docker volume inspect volume_name
  ```
  Displays detailed information about a Docker volume.

## Registry

- **Push Image to Registry:**
  ```bash
  docker push registry/image_name
  ```
  Pushes a Docker image to a registry.

- **Pull Image from Registry:**
  ```bash
  docker pull registry/image_name
  ```
  Pulls a Docker image from a registry.

## Tips and Tricks

- **Remove All Containers:**
  ```bash
  docker rm $(docker ps -a -q)
  ```
  Removes all stopped containers.

- **Remove All Images:**
  ```bash
  docker rmi $(docker images -q)
  ```
  Removes all Docker images.

- **Prune Unused Resources:**
  ```bash
  docker system prune
  ```
  Removes unused data, including stopped containers, networks, and dangling images.
```

Feel free to use this README.md formatted document for reference!
