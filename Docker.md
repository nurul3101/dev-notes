
## Docker

- Docker makes it easy to install and run software without worrying about setup or dependencies.
- Docker is a platform / ecosystem around creating and running containers.
- Docker ecosystem includes : Docker Client , Docker server , Docker Machine , docker hub , docker images, docker compose.
- When we execute a docker install command, docker cli goes to docker hub and installs a docker image on your harddrive.
- Docker Containers are instances of a docker image.
- Docker image is a file which contains dependencies and instructions to install a specific program
- --
- Docker Cli (client) is the software which we use to interact with docker daemon which is used to create containers and manage them.
- --
### what happens when we run 
```
docker run hello-world
```
The command is executed by docker-cli which does some pre-processing on it and passes it to docker server.
What we are saying is that we want to run a new container from an image named hello-world.
It will try to find the image in machine's local image cache, if image is not found then we reach out to docker hub to install the image.
Docker server downloaded the image from docker hub and stored it in image-cache.
Once the image is downloaded it is used to create a container which is an instance of the image.
Purpose of a container is to run a specific program,

---
### What is a container?

- Container isolates some portion of resources for a particular process.
- Docker image are the executables which at runtime are transformed into docker containers.
- Docker image is a combination of Filesystem snapshot and startup command.
- Containers internally uses namespacing (isolating resources per processes) and control groups (limit amount of resources used per process).
- Namespacing and control groups are portions of linux os.
- So when we installed docker for macOS/ windows and we start docker we have linux virtual machine running in our system.
- So this linux virtual machine is used to host these containers.
- When we executed `docker version` command it shows the os our docker server is running with.
- startup command is basically command which needs to be executed when a container is created. We can override the startup command of docker image.
---
### Dissecting docker commands

`docker run <img_name> command!`
docker - refers to the docker client (cli)
run - Try to **create** and **run** a container.
`docker run = docker create + docker run`
Docker create command just uses fs snapshot of image and prepares it so that it c
<image_name> - Name of the image to use for this container
E.g: `docker run busybox ls`
The override command that we enter depends upon the default filesystem of the docker-image.
For example ls executable was found in filesystem of busybox image so it was executed.

---

`docker ps` command lists all the running containers.
`docker ps --all` lists all the containers ever created.
`docker container prune` removes all stopped containers, and these containers will not be visible in docker ps --all command.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5ODE3NTAwNTYsLTI1MzMxOTczNyw1Mz
U0MDI1OTksOTg5MDkyOCwxNTE1Mzg4NDA0LDQ4NzI1MjI5OSwt
MjE0NTk3MTY3NSwtNDAzNzAxMTg3LDQ2NDU2MTY5MywtMTYxNj
Q1MzcxMSwtNTA0NDM1NzU1LDEyNTc0OTI0NDVdfQ==
-->