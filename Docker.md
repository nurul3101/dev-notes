
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


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMDIwMTg1NzAsLTQwMzcwMTE4Nyw0Nj
Q1NjE2OTMsLTE2MTY0NTM3MTEsLTUwNDQzNTc1NSwxMjU3NDky
NDQ1XX0=
-->