# Docker

Docker is a tool that allows you to run applications in an isolated environment similar to a virtual machine. It provides several benefits, such as ease of use and consistent behavior across different machines.

Some key advantages of Docker include:

- Rapid container creation, taking only seconds instead of minutes.
- Reduced resource consumption compared to virtual machines.
- Lower memory footprint.
- No need for a full operating system within the container.
- Simplified deployment and testing processes.

## Container vs Virtual Machine

Containers operate at the application layer, while virtual machines (VMs) abstract the entire operating system. Containers are lightweight and share the host OS kernel, resulting in faster startup times and lower resource usage.

## Docker Images and Containers

Docker uses images and containers to manage applications:

- **Image**: A template for creating an environment that includes everything your app needs to run (e.g., OS, dependencies, app code).
- **Container**: A running instance of an image.

### Commands

To interact with Docker, you can use the following commands:

- **Pull Images**: `docker pull <image name>:<version>`
- **List Images**: `docker images`
- **Remove Image**: `docker image rm <IMAGE ID>`
- **Run Container**: `docker run <image-name>:<version>`
  - Flags:
    - `-d`: Run in detached mode (in the background).
    - `-p <LOCAL_PORT>:<CONTAINER_PORT>`: Expose a port.
    - `--name <YOUR CONTAINER NAME>`
- **List Containers**: `docker container ls` or `docker ps`
  - Flags:
    - `-a`: List all containers.
- **Stop Container**: `docker stop <CONTAINER ID>`
- **Exposing Ports**: Use the `-p` flag with the `docker run` command to map ports between the host and the container.
- **Stop, Remove, and Rename Containers**:
  - Stop: `docker stop <CONTAINER ID>` or `docker stop <NAME>`
  - Start: `docker start <CONTAINER ID>` or `docker start <NAME>`
  - Remove: `docker rm <CONTAINER ID>` or `docker rm -f <CONTAINER ID>` (force removal)
  - Rename: `docker run --name <THE NAME YOU WANT> ...`

### Formatting Docker Output

You can format the output of the `docker ps` command using the `--format` flag, specifying the desired format.
Like `docker ps --format "table {{.ID}}\t{{.Image}}\t{{.Names}}\t{{.Status}}"`

## Volumes

Volumes allow data sharing between the host and containers, as well as between containers. They can be used for sharing files and folders.

To use volumes, employ the `-v <source>:<destination>:<mode-flag>` flag. For the destination, check the Docker Hub for details.

- **Host and Container**: 
  - Example: `docker run --name website -v $(pwd):/usr/share/nginx/html:ro -d -p 8080:80 nginx:latest`
  - Mode flags: `ro` (read-only), `rw` (read-write), `delegated`, `cached`, or `z`.
- **Container on Container**: 
  - Use `--volumes-from <name of second container>`.
  - Example: `docker run --name website-2 --volumes-from website -d -p=8081:80 nginx:latest`

## Dockerfile

A Dockerfile is a set of instructions to create an image. It allows you to define the steps required to set up your application environment.

Example Dockerfile:
```Dockerfile
FROM node:latest
WORKDIR /app
ADD . .
RUN npm install
CMD node index.js
```

### Docker Build

To build an image from a Dockerfile, use the `docker build` command:
```bash
docker build --tag <name>:<version> <path-to-dockerfile>
```

## Dockerignore

The `.dockerignore` file specifies which files to ignore when building the image using the Dockerfile.

Example `.dockerignore`:
```
node_modules
Dockerfile
.git
```

## Cache and Layers

Docker utilizes cache and layers to optimize image building. If a step changes in the Dockerfile, Docker rebuilds that step and all subsequent steps. To maximize caching, change the order of steps in the Dockerfile.

## Image Size

To reduce image size, consider using the `alpine` distribution, which provides smaller images.

Example:
```Dockerfile
FROM node:alpine
WORKDIR /app
ADD package*.json ./
RUN npm install
ADD . .
CMD node index.js
```

## Tags, Versioning, and Tagging

Tagging images allows you to assign meaningful names and versions to your images, avoiding breaking changes.

To tag an image:
```bash
docker tag <SOURCE_IMAGE_NAME>:<SOURCE_VERSION> <TO_IMAGE_NAME>:<TO_VERSION>
```

## Docker Registries
Let you store and distribute your Docker images.
Used in your CD/CI pipeline


### Providers
* Docker HUB
* quay.io
* Amazon ECR

## Docker inspect
You can see the full state of the running container

`docker inspect <DOCKER ID>`

## Docker logs
To see what is going on with your container

static: `docker logs <DOCKER ID>`
live (you need to use the `-f` flag): `docker logs -f <DOCKER ID>`

## Docker exec
To jump into the container 
static: `docker exec --interactive <DOCKER ID>`
live (you need to use the `-f` flag): `docker logs -f <DOCKER ID>`

## Links

- [Docker Hub](https://hub.docker.com)

