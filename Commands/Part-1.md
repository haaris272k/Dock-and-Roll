# Docker Notes Part-I

## Table of Contents
1. [Pulling an Image](#pulling-an-image)
2. [Running Images and Containers](#running-images-and-containers)
3. [Listing and Deleting Images and Containers](#listing-and-deleting-images-and-containers)
4. [Executing Commands in a Running Container](#executing-commands-in-a-running-container)
5. [Port Mapping](#port-mapping)
6. [Volume Mapping](#volume-mapping)
7. [Docker Information](#docker-information)
8. [Attach and Detach Mode](#attach-and-detach-mode)
9. [Building and Pushing an Image](#building-and-pushing-an-image)
10. [Working with Environment Variables in Docker](#working-with-environment-variables-in-docker)
11. [Entrypoints](#entrypoints)

---

## Pulling an Image
- `docker pull 'image_name'`: Pull an image.

## Running Images and Containers
- `docker run 'image_name'`: Start a container from the specified image.
- `docker run 'image_name' sleep 'n'`: Start a container with a specified sleep duration.
- `docker run -d 'image_name'`: Start a container in detach mode.
- `docker run -it 'image_name' bash`: Execute commands interactively in a running container.
- `docker run --name webapp -d nginx:1.14-alpine`: Start a named container.

## Listing and Deleting Images and Containers
- `docker images`: List images and their sizes.
- `docker ps`: List all running containers.
- `docker ps -a`: List all containers, including previously stopped ones.
- `docker stop 'container_id/name'`: Stop a running container.
- `docker rm 'container_id/name'`: Remove a container permanently.
- `docker container prune -f`: Remove all stopped containers.
- `docker rmi 'image_name'`: Delete an image.
- `docker rmi -f $(docker images -q)`: Remove all images (with stopped containers).

## Executing Commands in a Running Container
- `docker exec 'container_id/name' 'command_to_execute'`: Execute a command within a running container (e.g., view file contents).

## Port Mapping

Port mapping is a crucial concept in Docker that allows you to make web applications running inside a Docker container accessible from outside the host.

- **Command Syntax**: To map a host's port to the container's port for accessibility, use the following command:

  ```bash
  docker run -p 'host_port':'container_port' 'image_name'
- Note: Always stop the Docker service before mapping the port(s).

## Volume Mapping

Volume mapping allows you to persist data between the host and a Docker container. It's useful for storing configurations, databases, and other data that should survive container restarts.

- **Command Syntax**: To map a volume between the host and a container, use the following command:

  ```bash
  docker run -v 'host_path':'container_path' 'image_name'
- **Example**: Mapping a local directory to a container's `/app/data` directory:

  ```bash
  docker run -v /local/path:/app/data 'image_name'

- Note: Ensure that the host directory exists before using volume mapping.

## Docker Information
- `docker inspect 'container_name'`: Get detailed information about a Docker container.
- `docker logs 'container_id'`: View the logs of a container.

## Attach and Detach Mode
- "Attach" mode runs a container in the foreground.
- "Detach" mode runs a container in the background.

  ```bash
  docker run 'image_name'
  
  docker run -d 'image_name'

Building and Pushing an Image

To create a Docker image effectively, follow these steps:

    Understand Application Requirements
        Grasp your application's specific requirements.
        Structure the Dockerfile accordingly.
        Ensure it includes instructions for selecting a base image, copying files, configuring environment variables, and defining startup procedures.

    Create a Dockerfile

        Craft a Dockerfile with the necessary instructions.

        Here's a Dockerfile for a Go script that prints 'Hello World':

        Dockerfile

     # Use an official Go runtime as a parent image
     FROM golang:1.16
     
     # Set the working directory within the container
     WORKDIR /app
     
     # Copy the local Go script into the container's working directory
     COPY . /app
     
     # Compile the Go script
     # I have used hello.go as the name of the script
     RUN go build hello.go 
     
     # This line specifies the command that will run when a container based on this image starts
     # In this case, it runs the compiled Go binary
     CMD ["./hello"]

Build the Image

    Navigate to the directory containing the Dockerfile.

    Run the following command to build the image:

    shell

docker build -t 'image_name' .

After the image is built, you can verify its functionality by running the following command in the bash shell:

bash

    docker run 'image_name'

Push to DockerHub

    Tag your image with your DockerHub username and the desired version (optional).

    shell

docker tag 'image_name' 'dockerhub_username/'image_name':'version'

Log in to DockerHub if not already logged in:

shell

docker login

Push the image to DockerHub:

shell

        docker push 'dockerhub_username/'image_name':'version'

By following these steps, you can build a Docker image and push it to DockerHub for distribution.
Working with Environment Variables in Docker

Environment variables in Docker allow you to pass configuration values to containers at runtime. They are commonly used to provide settings, secrets, or application-specific data to your Dockerized applications.
Steps to Use Environment Variables

    Define Environment Variables in Dockerfile

        In your Dockerfile, set environment variables using the ENV instruction. For example:

        Dockerfile

    ENV APP_ENV production

Pass Environment Variables During Container Run

    When you run a container, use the -e or --env option to provide values for environment variables. For instance:

    bash

    docker run -e DATABASE_URL=postgres://user:password@localhost/dbname my-app-image

Access Environment Variables in Your Application

    In your application code, you can access environment variables easily.

        In Python:

        python

import os
db_url = os.environ.get("DATABASE_URL")

In Node.js:

javascript

            const dbUrl = process.env.DATABASE_URL;

Example

Let's say you have a web application that connects to a database. Instead of hardcoding the database connection details
User
(Part-1 -> Basic Commands, Port and Volume Mapping, Building and Pushing an Image, Environment Variables, and Entrypoint)

I wil lcreate separte .md files so is this cooretc to specify the part 1? or could it be mroe spcrifc?
ChatGPT

It's a good practice to specify a more specific title rather than just "Part-1" to make it clearer what each .md file contains. You can use titles that describe the main topics or sections covered in each file. For example:

    "Docker Basic Commands.md"
    "Port and Volume Mapping in Docker.md"
    "Building and Pushing Docker Images.md"
    "Working with Environment Variables in Docker.md"
    "Understanding Entrypoints in Docker.md"

This way, it will be easier for readers to navigate and understand the content of each file.


## Pulling an Image
- `docker pull 'image_name'`: Pull an image.

## Running Images and Containers
- `docker run 'image_name'`: Start a container from the specified image.
- `docker run 'image_name' sleep 'n'`: Start a container with a specified sleep duration.
- `docker run -d 'image_name'`: Start a container in detach mode.
- `docker run -it 'image_name' bash`: Execute commands interactively in a running container.
- `docker run --name webapp -d nginx:1.14-alpine`: Start a named container.

## Listing and Deleting Images and Containers
- `docker images`: List images and their sizes.
- `docker ps`: List all running containers.
- `docker ps -a`: List all containers, including previously stopped ones.
- `docker stop 'container_id/name'`: Stop a running container.
- `docker rm 'container_id/name'`: Remove a container permanently.
- `docker container prune -f`: Remove all stopped containers.
- `docker rmi 'image_name'`: Delete an image.
- `docker rmi -f $(docker images -q)`: Remove all images (with stopped containers).

## Executing Commands in a Running Container
- `docker exec 'container_id/name' 'command_to_execute'`: Execute a command within a running container (e.g., view file contents).

## Port Mapping

Port mapping is a crucial concept in Docker that allows you to make web applications running inside a Docker container accessible from outside the host.

- **Command Syntax**: To map a host's port to the container's port for accessibility, use the following command:

  ```bash
  docker run -p 'host_port':'container_port' 'image_name'
- Note: Always stop the docker service before mapping the port(s).

## Volume Mapping

Volume mapping allows you to persist data between the host and a Docker container. It's useful for storing configurations, databases, and other data that should survive container restarts.

- **Command Syntax**: To map a volume between the host and a container, use the following command:

  ```bash
  docker run -v 'host_path':'container_path' 'image_name'
- **Example**: Mapping a local directory to a container's `/app/data` directory:

  ```bash
  docker run -v /local/path:/app/data 'image_name'

- Note: Ensure that the host directory exists before using volume mapping.


## Docker Information
- `docker inspect 'container_name'`: Get detailed information about a Docker container.
- `docker logs 'container_id'`: View the logs of a container.

## Attach and Detach Mode
- "Attach" mode runs a container in the foreground.
- "Detach" mode runs a container in the background.
  
  ```bash
  docker run 'image_name'
  
  docker run -d 'image_name'

## Building and Pushing an Image

To create a Docker image effectively, follow these steps:

1. **Understand Application Requirements**
   - Grasp your application's specific requirements.
   - Structure the Dockerfile accordingly.
   - Ensure it includes instructions for selecting a base image, copying files, configuring environment variables, and defining startup procedures.
   
2. **Create a Dockerfile**
   - Craft a Dockerfile with the necessary instructions.
   
     Here's a Dockerfile for a go script that prints 'Hello World':
   
     ```Dockerfile
      # Use an official Go runtime as a parent image
      FROM golang:1.16
      
      # Set the working directory within the container
      WORKDIR /app
      
      # Copy the local Go script into the container's working directory
      COPY . /app
      
      # Compile the Go script
      # I have used hello.go as the name of the script
      RUN go build hello.go 
      
      # This line specifies the command that will run when a container based on this image starts
      # In this case, it runs the compiled Go binary
      CMD ["./hello"]


     ```

3. **Build the Image**
   - Navigate to the directory containing the Dockerfile.
   - Run the following command to build the image:
   
     ```shell
     docker build -t 'image_name' .
     ```
   - After the image is built, you can verify its functionality by running the following command in the bash shell:
     
      ```bash
      docker run 'image_name'

4. **Push to DockerHub**
   - Tag your image with your DockerHub username and the desired version (optional).
   
     ```shell
     docker tag 'image_name' 'dockerhub_username/'image_name':'version'
     ```
   
   - Log in to DockerHub if not already logged in:
   
     ```shell
     docker login
     ```
   
   - Push the image to DockerHub:
   
     ```shell
     docker push 'dockerhub_username/'image_name':'version'
     ```

By following these steps, you can build a Docker image and push it to DockerHub for distribution.

## Working with Environment Variables in Docker

Environment variables in Docker allow you to pass configuration values to containers at runtime. They are commonly used to provide settings, secrets, or application-specific data to your Dockerized applications.

### Steps to Use Environment Variables

1. **Define Environment Variables in Dockerfile**

   - In your Dockerfile, set environment variables using the `ENV` instruction. For example:
   
     ```Dockerfile
     ENV APP_ENV production
     ```

2. **Pass Environment Variables During Container Run**

   - When you run a container, use the `-e` or `--env` option to provide values for environment variables. For instance:
   
     ```bash
     docker run -e DATABASE_URL=postgres://user:password@localhost/dbname my-app-image
     ```

3. **Access Environment Variables in Your Application**

   - In your application code, you can access environment variables easily.
   
     - In Python:
       ```python
       import os
       db_url = os.environ.get("DATABASE_URL")
       ```
       
     - In Node.js:
       ```javascript
       const dbUrl = process.env.DATABASE_URL;
       ```

### Example

Let's say you have a web application that connects to a database. Instead of hardcoding the database connection details, you can use environment variables:

1. In your Dockerfile, set environment variables:

   ```Dockerfile
   ENV DB_HOST=localhost
   ENV DB_PORT=5432
   ENV DB_USER=myuser
   ENV DB_PASSWORD=mypassword

When running your container, you can pass environment variables to configure your application. Here's how you do it:

1. **Using Bash**
   - Run the container with the desired environment variables:

     ```bash
     docker run -e DB_HOST=database-server -e DB_USER=appuser my-app-image
     ```

2. **In Your Application Code (Python)**
   - In your application code, you can access these environment variables like this:

     ```python
     import os
     db_host = os.environ.get("DB_HOST")
     db_user = os.environ.get("DB_USER")
     ```
# Entrypoints

The `ENTRYPOINT` instruction in Docker specifies the command that will run when the container starts. It allows you to define the primary command or executable for your container.

- The command should either be in array format (e.g., `["sleep", "5"]`) or in normal format (e.g., `sleep 5`).
- When using `ENTRYPOINT`, any additional command line arguments provided when running the container will be passed as arguments to the specified command.

### Example

Suppose you have a Dockerfile for a simple Python script that prints a greeting:

```Dockerfile
FROM python:3

# Set the working directory
WORKDIR /app

# Copy the Python script into the container
COPY hello.py .

# Define the entry point
ENTRYPOINT ["python", "hello.py"]
```
hello.py file for this case looks like:

```python
import sys

# Get the command-line arguments
arguments = sys.argv[1:]

# Print the arguments
print("Hello,", " ".join(arguments))
```

In this example, the `ENTRYPOINT` specifies the primary command to execute when the container starts, and any arguments provided to `docker run` will be passed to `hello.py`.

```bash
docker run hello-app John
```
Output would be like:

```bash
hello, John
```