# Docker Manual

**Author:** Shadowdrums

## Table of Contents
1. [Installing Docker](#installing-docker)
2. [Installing Docker Compose](#installing-docker-compose)
3. [Managing Containers](#managing-containers)
4. [Working with Docker Images](#working-with-docker-images)
5. [Running Docker Containers](#running-docker-containers)
6. [Creating a Dockerfile](#creating-a-dockerfile)
7. [Using Docker Compose](#using-docker-compose)

---

## Installing Docker

To install Docker on your Linux system, follow these steps:

1. **Add Docker’s GPG Key:**
    ```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    ```

2. **Set Up the Stable Repository:**
    ```bash
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```

3. **Install Docker Engine:**
    ```bash
    sudo apt-get update
    sudo apt-get install -y docker-ce docker-ce-cli containerd.io
    ```

---

## Installing Docker Compose

1. **Download the Current Stable Release of Docker Compose:**
    ```bash
    sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    ```

2. **Apply Executable Permissions to the Binary:**
    ```bash
    sudo chmod +x /usr/local/bin/docker-compose
    ```

3. **Verify the Installation:**
    ```bash
    docker-compose --version
    ```

---

## Managing Containers

1. **Show All Running Containers:**
    ```bash
    docker ps -a
    ```

2. **Stop a Container:**
    ```bash
    docker stop <container name or ID>
    ```

3. **Remove a Container:**
    ```bash
    docker rm <container name or ID>
    ```

4. **Stop and Remove All Containers:**
    ```bash
    docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)
    ```

---

## Working with Docker Images

1. **Search for Docker Images:**
    ```bash
    docker search <image-name>
    ```

    Example:
    ```bash
    docker search ubuntu
    ```

2. **Pull a Docker Image:**
    ```bash
    docker pull <image-name>:<tag>
    ```

    Examples:
    ```bash
    docker pull ubuntu
    docker pull ubuntu:latest
    ```

3. **Verify You Have the Image:**
    ```bash
    docker images
    ```

---

## Running Docker Containers

1. **Run an Image Interactively:**
    ```bash
    docker run -it ubuntu
    ```

2. **Run an Image with a Specific Shell:**
    ```bash
    docker run -it ubuntu bash
    ```

3. **Run a Container in Detached Mode:**
    ```bash
    docker run -d ubuntu
    ```

4. **Run a Container with a Custom Name:**
    ```bash
    docker run -it --name <container name> ubuntu
    ```

---

## Creating a Dockerfile

A `Dockerfile` is a script that contains a series of instructions to build a Docker image. Here’s a simple example:

1. **Create a `Dockerfile`:**

    Example `Dockerfile`:
    ```Dockerfile
    # Use an official Ubuntu as a parent image
    FROM ubuntu:latest

    # Set the working directory in the container
    WORKDIR /app

    # Copy the current directory contents into the container at /app
    COPY . /app

    # Install any needed packages
    RUN apt-get update && apt-get install -y python3

    # Make port 80 available to the world outside this container
    EXPOSE 80

    # Run a command in the container
    CMD ["echo", "Hello, World!"]
    ```

2. **Build the Docker Image:**
    ```bash
    docker build -t my-custom-image .
    ```

---

## Using Docker Compose

Docker Compose allows you to define and manage multi-container Docker applications.

1. **Create a `docker-compose.yml` File:**

    Example `docker-compose.yml`:
    ```yaml
    version: '3'
    services:
      web:
        image: nginx
        ports:
          - "8080:80"
      app:
        build:
          context: .
          dockerfile: Dockerfile
        volumes:
          - .:/app
        ports:
          - "5000:5000"
    ```

2. **Build and Start the Containers:**
    ```bash
    docker-compose up --build
    ```

3. **Stop the Containers:**
    ```bash
    docker-compose down
    ```

This `README.md` should serve as a comprehensive guide for setting up, managing, and using Docker and Docker Compose on your system.

**Signed, Shadowdrums**

