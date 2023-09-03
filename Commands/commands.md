# Docker Command Notes

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


