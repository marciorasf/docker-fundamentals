# docker-study

## What is Docker

Docker is a software that providade several tools to work with containers with efficiency, both to the development perspective and the execution performance.

### What is a container

A container is a isolated environment used to run apps inside it. The "isolated" characteristic is essential to the idempotency provided by the use of containers, which means that no matter where the container is executed, the behavior should be the same.


### Container vs Virtual Machine

The main difference between **containers** and **virtual machines**, is that containers virtualize the **operating system**, while virtual machines virtualize the **hardware** to run multiple OS instances.

Consequently, the biggest advantage of using containers is the reduction of the overhead on storage, memory and CPU resources. This can achieved because each container doesn't have to have it own OS.

This advantage can be seen clearly when we compare the size and initialization. Most containers have only megabytes in size and take seconds do start, while VMs have gygabytes and take minutes to initialize.

### What is an image

A image is file compoused of several layers that works as instructions to create containers.

---

## Why use it

- Idempotency - ensures that the app has the same behavior independently of the environment.

- Faster development - the development environment can be set in some minutes on each machine.

- Quick and simple deploy - most cloud computer services accepts deploying container images.

- Sacalability - because the containers are self-contained, they can be replicated to scale apps.

---

## Basic components

### Docker Client

Docker Client is the way that users usually communicate with the Docker Engine.

### Docker Daemon

The Docker Daemon is responsible to listen for Docker Client requests and based on them, manage Docker objects such as images, containers, networks and volumes.

### Registry

A Docker registry stores Docker images. The default registry used with Docker is the Docker Hub, which is a kind of GitHub for Docker images.

---

## How to use

### Requirements 
Docker must be installed. The installation guide can be found [here](https://docs.docker.com/engine/install/ubuntu/).

### Create container
```bash
docker container run hello-world
```

Note that when this command is executed, the first line printed is (if you doesn't have this image on yout computer):

```bash
Unable to find image 'hello-world:latest' locally
```

After the message, the image starts to be downloaded. The download is made from Docker Hub. Following the container is created, the program is executed and then the process ends.

If you run the same command again, the image will be available locally, so it doesn't have to be downloaded again.

### Dettached mode
The hello-world container is created, executed and the finishes. But this is not the expected behavior for several other containers. Let's see an example using an nginx container.

```bash
docker container run nginx
```

After creating the container, you can see that the container stay alive (use **ctrl + c**, to stop the process). To not have to keep a terminal locked with this process, you can use the detach mode with the **-d** option.

```bash
docker container run -d nginx
```

After the container creation, the process exits and container keeps running on background.

### List containers

To see the your containers, use the following command:

```bash
docker container ls
```

If everything is all right until here, this command should list the dettached nginx container.

Note that the hello-world container are not listed, this occurs, because they're stopped. To list all containers use **-a** option.

```bash
docker container ls -a
```

Now you should see the other containers.

### Execute command on running container

You can execute commands inside containers:

```bash
docker exec <container_name|container_id> <command>
```

### Attach to running container

To attach to a container running on background use the **attach** command:

```bash
docker attach <container_name|container_id>
```

### Port bind

By default, the containers ports aren't accessible from outside docker. To overcome this problem, a port bind can be made using the **-p** option.

```bash
# docker container -p <pc_port>:<container_port> nginx
docker container run -p 8080:80 nginx
```

Now, a nginx welcome should be displayed on http://localhost:8080

### Interactive mode
Some containers can run in interactive mode. For example a ubuntu container that can open a terminal. To achieve this, you have to use the **-it** option.

```bash
docker container run -it ubuntu /bin/bash
```

Enter **exit** command to exit container.

### Stop container

To stop a container:

```bash
docker container stop <container_name|container_id>
```

### Remove container

When using Docker frequently, it's common that your pc ends up as a container cemetary. You can remove these dangling containers.

```bash
docker container rm <container_name|container_id>
```

You can pass more than one container too:

```bash
docker container rm <container_name|container_id> <container_name|container_id>
```

Other option is using **prune** to remove all stopped containers:

```bash
docker container prune
```

### Create image

#### Dockerfile

### Build image

### List images

### Push to Docker Hub

### Tag image

### Prune
