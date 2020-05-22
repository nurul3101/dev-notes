
## Docker

- Docker makes it easy to install and run software without worrying about setup or dependencies
- Docker is a platform / ecosystem around creating and running containers.
- Docker ecosystem includes : Docker Client , Docker server , Docker Machine , docker hub , docker images, docker compose.
- When we execute a docker install command, docker cli goes to docker hub and installs a docker image on your harddrive.
- Docker Containers are instances of a docker image.
- Docker image is a file which contains dependencies and instructions to install a specific program.
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
- *Docker image are the executables which at runtime are transformed into docker containers.*
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
`docker run [-it] <img_name> sh` will create a container and open a shell immediately
docker - refers to the docker client (cli)
run - Try to **create** and **run** a container.
`docker run = docker create + docker start`
Docker create command just uses fs snapshot of image and prepares it so that it can be ran later.
Docker start command executes  the startup command.
<image_name> - Name of the image to use for this container
E.g: `docker run busybox ls`
The override command that we enter depends upon the default filesystem of the docker-image.
For example ls executable was found in filesystem of busybox image so it was executed.

---

`docker ps` command lists all the running containers.
`docker ps --all` lists all the containers ever created.
`docker container prune` removes all stopped containers, and these containers will not be visible in docker ps --all command.
`docker create hello-world` just creates a container, does not run it. and returns the container id.
we can start the created container with
`docker start id_container` with optional `-a` flag to attach it to the container so that we can watch the output coming from the container.
`docker logs container_id` will show all the logs that have been emitted from that specified container. It will not start/ stop the container.
To stop a container: `docker stop container_id`
Docker stop command emits SIGTERM command to the process and allows some time for cleanup and exit.
If the container does not gracefully exit in 10 seconds then Docker emits SIGKILL command which eventually kills the container.
`docker kill conatiner_id` emits SIGKILL command and it stops instantly. 

---

 If a program is running inside a container, we cannot access that program from outside of container.
 E.g: `redis-server`  is running inside the container and if we execute `redis-cli` from outside the container terminal, then even though server is running, client will not be able to access it.

To execute a command in a docker container we use 
`docker exec [-it] [container_id] [command]`
-it flag is used to send input to the container.

Every Process in linux has three streams attached to it, STDIN , STDOUT, STDERR

-it flag is equivalent to -i , -t flag.
-i flag represents that we want to plug in this terminal to STDIN channel of the container and -t flag formats the output that is coming from the container.

- To start a shell in a container we can use
```
docker exec -it [container_id] sh
```
-  docker containers do not share the filesystem with other containers.

---

## Creating Dockerfile to create our own custom containers.

Specify a base image
Run some commands to install additional programs
Specify a command to run on container startup.

Dockerfile is a configuration file to define how our containers behave
Docker client passes on Dockerfile to docker server which creates a usable image.
*Image id and container id are different*
Example of a Dockerfile
```docker
# Use an existing image as a base
# Download and install a dependency
# Tell the image what to do when it starts as a container
FROM alpine
RUN apk add --update redis
CMD ["redis-server"]
```
To create an image from dockerfile we use command:
`docker build .` in the directory of Dockerfile
`.` is the build context
Docker file consists of Instruction telling docker server what to do and argument to the instruction.
Base image is kind of an OS which comes with some pre-installed packages which will be helpful for the task we wish to accomplish

When docker encountered RUN command it took the base image created in the previous step , created a new container with added program , took the snapshot of filesystem and deleted the intermediate container.
CMD command just added a startup command for the docker image.

Whenever we execute a build command it checks the cache if any intermediate container with the same steps is found it uses it.
The order of steps in dockerfile is extremely important, as it needs to execute all the commands below the changed/added step.

When we build an image from Dockerfile, it gives us the image_id which can be difficult to remember, so we can tag an image which will give it a human friendly name.
Example:
`docker build -t nurul3101/redis:latest .`  

We can take a snapshot of a running container and use it as an image for creating different containers using docker commit
Example:
`docker commit -c 'CMD ["redis-server"]' [container_id]`
will create a new image from the existing container.

alpine word in docker community ususally means it has the v=bare minimums required and no additional programs installed in the image.

By default none of the files in the project directory is available to container.
For copying the files we use 
`COPY source destination` command.
The path here is relative to build context.

By default network traffic to the local machine is not routed to the container's network, we need to explicitly route the request to the container with `-p` flag in `docker run`
```
docker run -p 8080:8080 nurul3101/node-docker:latest
```
will route requests from local machine's port 8080 to container's 8080 port. The ports does not need to be same.

By default when we copy files it is copied into the root directory which is not a good practice and instead we should have installed it in a specific folder, to address this we use
`WORKDIR` command in docker file.

There should be only one CMD command which works as a startup command for the container. 

To dele
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkwMzQ0ODQ3OCwxNjUxNDkxNTc1LC0xNz
MzMTAxNDk1LDExOTQwNTI4MTIsLTIxMjQyNjg4NDcsLTU2MTY5
NjA0NSw2MTkzMjI0OTUsMjAxMzg1MjkyNCwxMzU4NDIzMzgzLC
0xNTIyMjA2NTUyLDE1NzQyNjAwNDksLTUyNjEwNzE2MSwtMTUx
MDY1MjI5LC0zNTk5OTgzOCwtNjk4MjQwMTkyLDgxMDM5MDczMi
wzODg0MjcyNzAsLTk0NTgyODQ1MSwtMjExNTA1MDQzNSwtMTUz
ODMwNDgwN119
-->