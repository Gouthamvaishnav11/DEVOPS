## Docker: An Overview

# What is Docker?

Docker is an open-source platform that uses OS-level virtualization to deliver software in packages called containers. Containers are lightweight, portable, and self-sufficient units that package an application's code, libraries, dependencies, and configuration files together. Think of it as "build once, run anywhere" – ensuring consistency across development, testing, and production environments. It's a key technology in modern DevOps practices, enabling Continuous Integration/Continuous Deployment (CI/CD) pipelines.

# Why Use Docker? (Advantages)

  - Consistency: Eliminates the "it works on my machine" problem by ensuring the application runs the same way everywhere.
  - Isolation: Containers isolate applications from each other and from the underlying infrastructure, preventing conflicts between dependencies.
  - Portability: Docker containers can run on any machine that has the Docker Engine installed (Linux, Windows, macOS, cloud providers).
  - Lightweight & Fast: Containers share the host OS kernel, making them much smaller and faster to start than traditional virtual machines (VMs).
  - Resource Efficiency: Requires fewer system resources (CPU, memory, storage) compared to VMs.
  - Scalability: Easy to scale applications horizontally by spinning up multiple container instances.
  - Rapid Deployment: Containers can be created and deployed very quickly.
  - Version Control & Rollback: Docker images can be versioned, and containers can be easily rolled back to previous stable states.
  - Improved Security: While sharing the kernel, containers provide process and network isolation, enhancing security compared to running applications directly on the host.
---
# Limitations (Disadvantages)

- Security Risks: Sharing the host OS kernel can be a potential vulnerability if a container is compromised. Requires careful security practices (e.g., minimal base images, least privilege).
- Complexity: Can add complexity to the overall architecture and operational processes, especially for teams new to containerization.
- Performance Overhead (Minor): While much better than VMs, there is still a slight performance overhead compared to running natively on the host OS kernel.
- Learning Curve: Requires understanding container concepts, Docker commands, and potentially orchestration tools.
- State Management: Managing persistent data (state) requires careful planning, often using Docker Volumes or Bind Mounts.
---

## Architecture of Docker:

- <img src="https://github.com/user-attachments/assets/a4d5f8de-e06b-4b35-94ad-7ad9812d7137" alt="image" width="300"/>


## Components of Docker:
# Docker Daemon:
-Docker daemon runs on the Host O.S.
-It is responsible for running containers, and managing docker services.
-Docker daemons can communicate with other daemons.

# Docker Client: 
-Docker users can interact with the docker daemon through a client.
-Docker client uses commands and Rest API to communicate with the docker
daemon.
-When a client runs any server command on the docker client terminal, the
client terminal sends the docker commands to the docker daemon.
-Docker clients can communicate with more than one daemon.

# Docker Host
Docker Host is used to providing an environment to execute and run
applications. It contains the docker daemon, images, containers, networks,
and storage.

# Docker Hub/Registry:
Docker registry manages and stores the docker images.
There are two types of registries in the docker.

1) Public Registry → Public registry also called Docker Hub.
2) Private Registry → It is used to share images within the enterprise

# Docker images:
Docker images are the read-only binary templates used to create docker
containers. or, a single file with all dependencies and configurations
required to run a program.
→ Ways to create an images:
   1.Take an image from Docker Hub.
   2.Create an image from Docker File.
   3.Create an image from existing docker containers.

## Docker Image Commands

Images are read-only templates used to create containers. They contain the application code, libraries, tools, settings, and runtime needed to run the application.

```bash
# 1. List all Docker images locally
docker images
# or
docker image ls

# 2. Pull an image from a registry (default is Docker Hub)
docker pull <image_name>[:<tag>]
# Example: Pull the latest Ubuntu image
docker pull ubuntu
# Example: Pull a specific tagged Nginx image
docker pull nginx:1.25-alpine

# 3. Build an image from a Dockerfile in the current directory
docker build -t <image_name>[:<tag>] [OPTIONS] .
# Example: Build an image named 'my-web-app' with tag 'v1'
docker build -t my-web-app:v1 .
# Example: Build using a specific Dockerfile name
docker build -f Dockerfile.dev -t my-app:dev .

# 4. Tag an existing image (create an alias)
docker tag <source_image_name>[:<tag>] <target_image_name>[:<tag>]
# Example: Tag 'my-web-app:v1' to also be 'latest'
docker tag my-web-app:v1 my-web-app:latest

# 5. Push an image to a registry
docker push <image_name>[:<tag>]
# Example: Push 'my-web-app:latest' to Docker Hub (requires login)
docker push my-web-app:latest

# 6. Show detailed information about an image
docker inspect <image_name>[:<tag>] | <image_id>
# Example: Inspect the 'nginx' image
docker inspect nginx

# 7. Remove one or more images
docker rmi <image_name>[:<tag>] | <image_id> [more_images...]
# Example: Remove the 'my-web-app:v1' image
docker rmi my-web-app:v1
# Example: Remove an image by ID
docker rmi a1b2c3d4e5f6

# 8. Remove unused images ( dangling <none> images by default )
docker image prune [OPTIONS]
# Example: Remove all unused images (both dangling and unreferenced)
docker image prune -a

# 9. History of an image (view layers and creation details)
docker history <image_name>[:<tag>] | <image_id>
# Example: See the history of the 'ubuntu' image
docker history ubuntu
```
# Docker Container :
 -The container holds the entire package that is needed to run the application.
or,
-In other words, we can say that the image is a template and the container is
a copy of that template.
-container is like virtualization when they run on the Docker engine.
-Images become containers when they run on the docker engine.
```
# 1. List all containers (running and stopped)
docker ps -a
# or
docker container ls -a
# Example: List only running containers
docker ps

# 2. Run a new container
docker run [OPTIONS] <image_name>[:<tag>] <command>
# Common OPTIONS:
#   -it              : Run in interactive mode with pseudo-TTY
#   --name <name>    : Assign a name to the container
#   -d               : Run container in detached mode (background)
#   -p <host_port>:<container_port> : Publish a container's port(s) to the host
#   -P               : Publish all exposed ports to random ports on the host
#   -v <host_path>:<container_path>[:<options>] : Mount a volume (bind mount)
#   --network <network_name> : Connect to a specific network
#   --rm             : Automatically remove the container when it exits
#   -e <key>=<value> : Set environment variables
# Example: Run an interactive Ubuntu shell
docker run -it ubuntu bash
# Example: Run Nginx in detached mode, map port 8080 on host to 80 in container, name it 'my_nginx'
docker run -d -p 8080:80 --name my_nginx nginx
# Example: Run a container that auto-removes itself after exit
docker run --rm busybox ping localhost

# 3. Start a stopped container
docker start <container_name> | <container_id> [more_containers...]
# Example: Start the container named 'my_nginx'
docker start my_nginx

# 4. Stop a running container
docker stop <container_name> | <container_id> [more_containers...]
# Example: Stop the container named 'my_nginx'
docker stop my_nginx

# 5. Restart a container
docker restart <container_name> | <container_id> [more_containers...]
# Example: Restart the container named 'my_nginx'
docker restart my_nginx

# 6. Execute a command in a running container
docker exec [OPTIONS] <container_name> | <container_id> <command>
# Common OPTIONS:
#   -it              : Run in interactive mode with pseudo-TTY
# Example: Get an interactive bash shell inside the 'my_nginx' container
docker exec -it my_nginx bash
# Example: Check the logs within the container
docker exec my_nginx tail -n 20 /var/log/nginx/error.log

# 7. Show detailed information about a container
docker inspect <container_name> | <container_id>
# Example: Inspect the 'my_nginx' container
docker inspect my_nginx

# 8. Remove one or more containers
docker rm <container_name> | <container_id> [more_containers...]
# Example: Remove the stopped container with ID 'a1b2c3d4e5f6'
docker rm a1b2c3d4e5f6
# Example: Force remove a running container (use with caution!)
docker rm -f my_nginx

# 9. Remove all stopped containers
docker container prune

# 10. Log into a running container (attaches stdin/stdout/stderr)
docker attach <container_name> | <container_id>
# Example: Attach to the 'my_nginx' container
docker attach my_nginx
# (Press Ctrl+P, then Ctrl+Q to detach without stopping the container)

# 11. View logs generated by a container
docker logs <container_name> | <container_id> [OPTIONS]
# Common OPTIONS:
#   -f               : Follow log output (tail -f)
#   --tail <number>  : Show only the last 'number' lines
#   -t               : Add timestamps to output
# Example: Follow the logs of 'my_nginx'
docker logs -f my_nginx
# Example: Show the last 10 lines of logs for 'my_nginx'
docker logs --tail 10 my_nginx

# 12. Copy files/folders between the host and a container
docker cp <source> <container_name>:/destination
docker cp <container_name>:/source <destination>
# Example: Copy 'local_file.txt' into 'my_nginx' container's '/tmp/' directory
docker cp local_file.txt my_nginx:/tmp/
# Example: Copy 'my_nginx' container's '/etc/nginx/nginx.conf' to the host's current directory
docker cp my_nginx:/etc/nginx/nginx.conf .

# 13. Commit changes in a container to create a new image
docker commit <container_name> | <container_id> <new_image_name>[:<tag>]
# Example: Commit changes in 'my_modified_container' to create 'my_updated_image:latest'
docker commit my_modified_container my_updated_image:latest
```
# Dockerfile Creation:
Docker image creation using existing docker file

-We have to create a container from our image, therefore create one
container first—

```sh
docker run -it --name <container_name><image_name> /bin/bash
```
```sh
cd tmp /[inside directory to create a file ]
```
-Now create one file inside this tmp directory
```sh
touch myfile
```
-Now if you want to see the difference between the base image & changes on it
then—
```sh
docker diff <old_container_name > [D->deletion, C->change , A->Append/Addition]
```
-Now create an image of this container
```sh
docker commit <container_name> <container_img_name>

docker images
```
- Now create a container from this image.
  ```sh
  docker run -it --name<container_name> <update_img_name> /bin/bash--> ls--> cd tmp/--> lso/p -->myfile[you will get all files back]
  ```
 --- 
# Dockerfile Creation using Dockerfile

# Dockerfile
-Dockerfile is a text file it contains some set of instruction.
-Automation of docker image creation.

# FROM
-For the base image. This command must be on top of the docker file.

# RUN
-To execute commands, it will create a layer in the image.
# MAINTAINER
-Author/Owner/Description
# COPY
-Copy files from the local system (dockerVM) we need to provide a source,
and destination. (We can’t download the file from the internet and any
remote repo)
# ADD
-Similar to copy, it provides a feature to download files from the internet,
-also we extract the file from the docker image side.
# EXPOSE
-To expose ports such as port 8080 for tomcat, port

# WORKDIR
- To set a working directory for a container.
# CMD
- Execute commands but during container creation.
# ENTRYPOINT
- Similar to CMD, but has higher priority over CMD, the first commands will be
executed by ENTRYPOINT only.
# ENV
- Environment Variables.

# ARG
- To define the name of a parameter and its default value, the difference
between ENV and ARG is that after you set on env. using ARG, you will not
be able to access that late on when you try to run the Docker container.


## Creation of Dockerfile
- Create a file named Dockerfile
- Add instructions in Dockerfile
- Build dockerfile to create an image
- Run image to create the container

```sh
[root@ip...]# vi Dockerfile
FROM ubuntu
RUN echo "Creating our Image" > /tmp/testfile
```

---

# To Create an Image out of Dockerfile

```sh
docker build -t <image_name> .
```
`-t <image_name>` → tags the image with a name.
* `.` → means the current directory where the Dockerfile is located.

---

# Check Process State

```sh
docker ps -a
```
-Lists all containers (running and stopped).

---

# See Images

```sh
docker images
```

- Lists all locally stored images.

---

# To Create a Container from the Above Image

```sh
docker run -it --name <container_name> <image_name> /bin/bash
```

- `-it` → interactive terminal.
-  `--name` → names your container.
-   `/bin/bash` → opens a shell in the container.

---

#Perfect! Let’s **write your Dockerfile creation steps** in **that same style**, structured like your screenshot—clear steps, code blocks, and short explanations. Here’s the text rewritten like your image example:

---

# 4. Run Image to Create the Container

```bash
[root@ip...]# vi Dockerfile

FROM ubuntu
RUN echo "Creating our Image" > /tmp/testfile
```

---

# To Create an Image out of Dockerfile

```bash
docker build -t <image_name> .
```

* `-t <image_name>` → tags the image with a name.
* `.` → means the current directory where the Dockerfile is located.

---

# Check Process State

```bash
docker ps -a
```

* Lists all containers (running and stopped).

---

## See Images

```bash
docker images
```

* Lists all locally stored images.

---

# To Create a Container from the Above Image

```bash
docker run -it --name <container_name> <image_name> /bin/bash
```

* `-it` → interactive terminal.
* `--name` → names your container.
* `/bin/bash` → opens a shell in the container.

---

# Ex. Command for Next Image Creation
  -No need to create a new Dockerfile—we can update the existing one:

```sh
[root@ip...]# vi Dockerfile
FROM ubuntu
WORKDIR /tmp
RUN echo "Hello World" > /tmp/testfile
ENV myname DevOps_Brother
COPY testfile /tmp
ADD test.tar.gz /tmp
```
---
- Open Dockerfile with vi remove all and this code
- We have to create a testfile, test, and test.tar.gz
- Then build the image
- Then create the image

-<img src="https://github.com/user-attachments/assets/f87fdb1b-8f75-44dc-bbd2-94715a33e82f" alt="image" width="400"/>

## All about Docker Volume
- Volume is simply a directory inside our container.
- Firstly, we have to declare this directory as a volume and then share the
volume.
- Even if we stop the container, still we can access volume.
- The volume will be created in one container.
- You can declare a directory as a volume only while creating the container.
- You can’t create volume from the existing container.
- You can share one volume across any number of containers.
- The volume will not be included when you update an image.
- We can map volume in two ways—
    1.Container ← → Container
    2.Host ← → Container
-<img src="https://github.com/user-attachments/assets/25dcae4c-c948-4e2e-b946-a7208244995d" alt="image" width="400"/>

## Benefits of Volume
- Decoupling container from storage.
- Share volume among different containers.
- Attach the volume to containers
- On deleting the container, the volume does not delete.

---


## 📦 Creating Volume from Dockerfile

---

#  Create a Dockerfile and Write

```dockerfile
FROM ubuntu
VOLUME ["/myvolume1"]
```
- This defines a **volume** named `/myvolume1` inside the container.

---

#  Build an Image from the Dockerfile

```bash
docker build -t <image_name> .
```

-  Replace `<image_name>` with the name you want for your Docker image.

---

# Create a Container from the Image and Run

```bash
docker run -it --name <container_name> <image_name> /bin/bash
```

-This starts a container from the newly built image.
-Replace `<container_name>` and `<image_name>` with your chosen names.

---

#  Check the Volume

Inside the running container, run:

```bash
ls
```

-  You will see the folder `/myvolume1` created automatically as a volume.

---

#   Share Volume with Another Container (Container ↔ Container)

To run a **second container** that shares the volume from the first container:

```bash
docker run -it --name <new_container_name> \
    --privileged=true \
    --volumes-from <existing_container_name> \
    <os_image_name> /bin/bash
```

-  `--volumes-from` → shares all volumes from the existing container.
-  Replace:

  * `<new_container_name>` → name for the second container
  * `<existing_container_name>` → name of the first container
  * `<os_image_name>` → e.g. `ubuntu`

---

* After creating **container2**, the volume `/myvolume1` is visible.
* Whatever you do inside the volume in one container can be seen from another container.

---

## ✅ Example Workflow

Here’s how it all comes together:

```bash
# 1. Create Dockerfile
vi Dockerfile

# Contents of Dockerfile:
# FROM ubuntu
# VOLUME ["/myvolume1"]

# 2. Build the image
docker build -t myvolume-image .

# 3. Run the first container
docker run -it --name mycontainer1 myvolume-image /bin/bash

# Inside container, check:
ls

# 4. Run a second container sharing the same volume
docker run -it --name mycontainer2 \
    --privileged=true \
    --volumes-from mycontainer1 \
    ubuntu /bin/bash
```

---


## Create volume by using the command

---

# create volume by using the command

```bash
docker run -it --name <container_name> -v /<volume_name> <os_name> /bin/bash
```

* Then do ls and change directory to your volume

---

# Now create one more container and save volume

```bash
docker run -it --name <container_name> --privileged=true --volumes-from <container_name> <os_name> /bin/bash
```

* Now you are inside the container; do ls, and you can see your volume
* Now create one file inside this volume and then check in containers, you can see that file.

---

# Volumes \[Host ↔ Container]

* Verify files in `/home/ec2-user`
* Create volumes in host and container and mapped them

```bash
docker run -it --name <container_name> -v /home/ec2-user/:/<volume_name> --privileged=true <os_name> /bin/bash
[Check your volume] ~ cd /<volume_name> [Do ls, now you can see all files of host machine] ~ touch <file_name>
```

* Now check in ec2, you can see the files.

---

## Some other commands:

---
# To see all created volumes

```bash
docker volume ls
```

---

# To create docker volume (normal)

```bash
docker volume create <volume_name>
```

---

# To delete volume

```bash
docker volume rm <volume_name>
```

---

# To remove all unused docker volumes

```bash
docker volume prune
```

---

# To get volume details

```bash
docker volume inspect <volume_name>
```

---

# To get container details

```bash
docker container inspect <container_name>
```

---

## Some other imp. Terms
# The difference between docker attach and docker exec
 - Docker exec creates a new process in the container’s environment while
    docker attaches just connect the standard I/O of the main process inside
    the container to the corresponding standard I/O error of the current
    terminal.
-  docker exec is especially for running new things in an already started
container, be it a shell or some other process.

# The difference between expose and publish a docker
- We have three options:

  1.Neither specifies expose nor -p
  
  2. Only specify expose
  
  3.Specify expose and -p

# Explain
  - If we specify neither expose nor -p the service in the container will only
      be accessible from inside the container itself.
    
-  If we expose a port, the service in the container is not accessible from
        outside docker, but from inside other docker containers, so this is good
            for inter-container communication.
   
-  If we expose and -p a port, the service in the container is accessible from
        anywhere, even outside docker.


# Docker vs. Virtual Machines (VMs) & Docker Networking

## Docker vs. Virtual Machines (VMs)

While both Docker containers and traditional Virtual Machines (VMs) provide a way to isolate applications, they do so in fundamentally different ways, leading to significant differences in resource usage, performance, and management.

| Feature           | Docker Container                                    | Virtual Machine (VM)                                      |
| :---------------- | :-------------------------------------------------- | :-------------------------------------------------------- |
| **Isolation**     | OS-level isolation. Shares the host OS kernel.      | Hardware-level isolation. Each VM includes a full guest OS. |
| **Size**          | Very small (MBs). Contains only app code, libs, config. | Much larger (GBs). Includes guest OS, hypervisor, apps.   |
| **Startup Time**  | Very fast (milliseconds/seconds).                   | Slower (seconds/minutes).                                 |
| **Resource Usage**| Highly efficient. Shares host kernel, uses less RAM/CPU. | Less efficient. Each VM needs its own OS and resources.    |
| **Portability**   | Highly portable across different environments.      | Portable, but image size is larger.                       |
| **Operating System**| Runs on a single, shared host OS kernel.           | Requires a full guest OS for each VM.                    |
| **Hypervisor**    | Not required (uses OS-level features).             | Requires a hypervisor (Type 1 like VMware ESXi, Type 2 like VirtualBox). |
| **Use Case**      | Ideal for microservices, application packaging, CI/CD. | Ideal for running entirely different OSes, full system isolation. |

**In simple terms:** Think of VMs as fully equipped apartments (each with its own kitchen, plumbing, etc.), while Docker containers are like rooms within a shared house that use the house's central utilities (the host OS kernel).

## Docker Networking

Docker provides robust networking capabilities to allow containers to communicate with each other, with the outside world, and with the host machine. It abstracts away the underlying network configuration details.

### Key Concepts:

1.  **Docker Network Driver:** The mechanism used to create and manage networks. Docker provides several built-in drivers:
    *   **Bridge:** The default network driver. Containers on the same bridge network can communicate, but not with containers on other bridge networks (unless explicitly linked or using user-defined bridges). User-defined bridges (created using `docker network create`) offer better isolation and features than the default bridge.
    *   **Host:** Container shares the network stack of the host machine. No network isolation. Useful for performance-sensitive applications where network overhead is critical.
    *   **None:** Container has no network interface configured. Network access is disabled.
    *   **Overlay:** Used to connect containers across multiple Docker daemon nodes (e.g., in a Swarm cluster). Requires a shared key-value store (like etcd, Consul) and often encryption.
    *   **MACVLAN:** Allows containers to have their own MAC address and appear as physical devices on the host network, using the host's IP address range.

2.  **User-Defined Bridge Networks:** Recommended over the default bridge. They provide:
    *   **Automatic DNS resolution:** Containers can resolve each other by name.
    *   **Improved isolation:** Better separation between different bridge networks.
    *   **Port sharing isolation:** Ports can be shared across containers on the *same* user-defined bridge network without conflict (e.g., multiple containers on port 80).

3.  **Docker Network Commands:**

```bash
# List all networks
docker network ls

# Show detailed information about a specific network
docker network inspect <network_name_or_id>

# Create a new network (default is 'bridge' driver)
docker network create [OPTIONS] <network_name>

# Example: Create a user-defined bridge network
docker network create --driver bridge my_custom_bridge

# Example: Create an overlay network (for Swarm)
# docker network create --driver overlay my_overlay_network

# Connect a running container to a network
docker network connect <network_name_or_id> <container_name_or_id>

# Disconnect a container from a network
docker network disconnect <network_name_or_id> <container_name_or_id>

# Remove one or more networks
docker network rm <network_name_or_id> [<network_name_or_id> ...]

# Remove all networks not used by at least one container
docker network prune




