---
description: This page provides installation and configuration information for Docker.
---

# Docker

## Confirming Docker is installed correctly

> **_NOTE:_** Note: Apple M1 devices:
At the time of writing there are some issues on Apple M1 devices and, some ARM64/ARMv8 devices. Please review [this forum thread](https://forums.ironmansoftware.com/t/docker-image-not-working/8781/15) before proceeding.

### Docker
Run the following command to confirm Docker is installed:
```
docker version
```

Example Output:
```
Client: Docker Engine - Community
 Version:           23.0.1
 API version:       1.42
 Go version:        go1.19.5
 Git commit:        a5ee5b1
 Built:             Thu Feb  9 19:47:01 2023
 OS/Arch:           linux/amd64
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          23.0.1
  API version:      1.42 (minimum version 1.12)
  Go version:       go1.19.5
  Git commit:       bc3805a
  Built:            Thu Feb  9 19:47:01 2023
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.6.18
  GitCommit:        2456e983eb9e37e47538f59ea18f2043c9a73640
 runc:
  Version:          1.1.4
  GitCommit:        v1.1.4-0-g5fd4c4d
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0

```
### Docker Compose
Docker Compose v1 uses the command `docker-compose`. As of June 2023 support ends for Docker Compose v1.

Docker Compose v2 uses the command `docker compose`. 

If you are using Docker Compose v1 please adjust the commands accoridingly. More infromation on Docker Compose can be found [here](https://docs.docker.com/compose/).

Run one of the following commands to check Docker Compose is installed:

Docker Compose v1:
```
docker-compose version
```
Docker Compose v2:
```
docker compose version
```
Example Output:
```
Docker Compose version v2.16.0
```

### A Docker Hello-World
To ensure that Docker has the ability to pull and run container images run the following command:
```
docker run hello-world
```
Example Output:
```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:ffb13da98453e0f04d33a6eee5bb8e46ee50d08ebe17735fc0779d0349e889e9
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

## Installation

## Using the pre-built Container

In order to run PowerShell Universal, you can use the provided container image. The docker image is available on [Docker Hub](https://hub.docker.com/r/ironmansoftware/universal) .

The prebuilt version allows you to run all free and paid features of PowerShell Universal.

You can start the container by pulling the image and then running a container with the default port bound.

### Running a basic image

```
docker pull ironmansoftware/universal
docker run --name 'PSU' -it -p 5000:5000 ironmansoftware/universal
```

### Present an image to a different port

If port 5000 is unavailable on your host, this can be switched to another port.

e.g. Present on port 80

``` 
docker pull ironmansoftware/universal
docker run --name 'PSU' -it -p 80:5000 ironmansoftware/universal
```

### Mount a volume

The `docker run` command will allow you to mount a volume for persistent storage. This needs to be mounted to the /root folder.

#### Mount a volume on container in  Windows 

The following command mounts the folder `C:\docker\volumes\PSU` to `/root` on your container

```
docker pull ironmansoftware/universal
docker run --name 'PSU' -it -p 5000:5000 ironmansoftware/universal -v C:\docker\volumes\PSU:/root
```

#### Mount a volume on Container on Mac and Linux
The following command mounts the folder `/docker/volumes/PSU` to `/root` on your container

```
docker pull ironmansoftware/universal
docker run --name 'PSU' -it -p 5000:5000 ironmansoftware/universal -v /docker/volumes/PSU:/root
```

### Stopping a Container
The following command removes a stopped container named `PSU`
```
docker stop PSU
```

### Removing a Container
The following command stops a container named `PSU`
```
docker rm PSU
```

The `--force` flag can be used to remove a running container
```
docker rm --force PSU
```

## Docker Compose
Docker Compose allows you to use a yaml text file to standardize your build and script the deployment (or build) or multiple containers.

The default name for any compose file is `docker-compose.yml` it is recommended you use this as your compose filename.

### Creating a Compose Script for Windows
The following compose file will run a Powershell Universal container in Windows

``` yml
version: "3.7"
services:
  PSU:
    container_name: PSU
    image: ironmansoftware/universal:latest
    ports:
      - 5000:5000
    restart: unless-stopped
    environment:
      - TZ=Europe/London
    volumes:
      - C:\docker\volumes\PSU:/root
```

### Creating a Compose Script for Mac / Linux
The following compose file will run a Powershell Universal container on Mac's and Linux

``` yml
version: "3.7"
services:
  PSU:
    container_name: PSU
    image: ironmansoftware/universal:latest
    ports:
      - 5000:5000
    restart: unless-stopped
    environment:
      - TZ=Europe/London
    volumes:
      - /docker/volumes/PSU:/root
```

### Starting  Containers using Compose Scripts
Using a Terminal shell, or PowerShell for Windows. cd to the directory with your `docker-compose.yml` script.

Run the following command
```
docker compose up -d
```
Example Output:
```
Creating network "PSU_default" with the default driver
Pulling PSU (ironmansoftware/universal:latest)...
latest: Pulling from ironmansoftware/universal
7608715873ec: Pull complete
4e66273c6cfb: Pull complete
2649c52300c2: Pull complete
a20175666bc7: Pull complete
65ce93bc0653: Pull complete
Digest: sha256:d7ff98e6197d21070aac325c2efbefa393a4952d2e8ba6b1327dc97824ec4d55
Status: Downloaded newer image for ironmansoftware/universal:latest
Creating PSU ... done
```

### Stopping Containers using Compose Scripts

Using a Terminal shell, or PowerShell for Windows. cd to the directory with your `docker-compose.yml` script.

Run the following command
```
docker compose down
```
Example Output:
```
[+] Running 2/2
 ⠿ Container PSU         Removed                                           0.5s
 ⠿ Network PSU_default   Removed                                           0.4s
```
### Using Environment Variables and SQL Persistance
You can add Environment variables into your Compose Scripts.
Below is an example of:
- Setting a node name
- Adding SQL persistance
- Adding a SQL Connection String

``` yaml
version: "3.7"
services:
  PSU:
    container_name: PSU
    image: ironmansoftware/universal:latest
    ports:
      - 5000:5000
    restart: unless-stopped
    environment:
      - TZ=Europe/London
      - Plugins:0=SQL
      - Data__ConnectionString = "Data Source=ServerName; Initial Catalog=DatabaseName; User Id=UserName; Password=UserPassword;"
      - NodeName=mynodename
    volumes:
      - /docker/volumes/PSU:/root
```

## Building a Custom Container

In some cases, you may wish to build more features, modify, or hardcode Environment Variables into your container.

For that, you will need to Create a `Dockerfile`

> **_NOTE:_** Dockerfiles' are case-sensitive and must start with a capital 'D'.

To create a Docker image that can persist the Universal data, you can create a dockerfile like the one below.

This Dockerfile exposes port 5000, creates a /data volume, sets configuration environment variables to store the Universal repository and database in the volume and then sets the Universal.Server as the entry point to the container.

### Writing a Dockerfile script for Linux
```
FROM ironmansoftware/universal:latest
LABEL description="Universal - The ultimate platform for building web-based IT Tools" 

EXPOSE 5000
VOLUME ["/home/data"]
ENV Data__RepositoryPath /home/data/Repository
ENV Data__ConnectionString /home/data/database.db
ENV UniversalDashboard__AssetsFolder /home/data/UniversalDashboard 
ENV Logging__Path /home/data/logs/log.txt
ENTRYPOINT ["./Universal/Universal.Server"]
```
### Building a container

From the path your Dockerfile is hosted in run the following command:

```
docker build . --tag=universal-persistent
```

### Windows

```
FROM ironmansoftware/universal:1.3.1-windowsservercore-1809
LABEL description="Universal - The ultimate platform for building web-based IT Tools" 

EXPOSE 5000
VOLUME ["C:/data"]
ENV Data__RepositoryPath C:/data/Repository
ENV Data__ConnectionString C:/data/database.db
ENV UniversalDashboard__AssetsFolder C:/data/UniversalDashboard 
ENV Logging__Path C:/data/logs/log.txt
ENTRYPOINT ["C:/ProgramData/Universal/Universal.Server.exe"]
```

You can run a build with the build command.

```
docker build . --tag=universal-persistent
```

You can start the docker container with the run command and make sure to specify the volume to mount.

```
docker run -it --name powershelluniversal --mount source=psudata,target=/home/data --rm -d  -p 5000:5000/tcp universal-persistent:latest
```

### SQL

To use SQL persistence, you can define the plugin and connection string as follows.&#x20;

```
ENV Data__ConnectionString=Data Source=ServerName; Initial Catalog=DatabaseName; Integrated Security=SSPI;
ENV Plugins:0=SQL
```

## Time Zones

To properly support time zones on Linux when scheduling jobs, you will need to include the `tzdata` package in your dockerfile along with an environment variable that specifies the server time zone.&#x20;

```
ENV TZ Europe/Amsterdam
RUN apt-get install -y tzdata
```

# Summary

This has been a very basic "How get get started" which allows you to get started running or building PSU Containers. All souces for commands have been linked in the referances session.

# References
## Running Containers
https://docs.docker.com/engine/reference/commandline/run/

https://docs.docker.com/engine/reference/commandline/stop/

https://docs.docker.com/engine/reference/commandline/rm/

https://docs.docker.com/compose/

## Building Containers
https://docs.docker.com/engine/reference/commandline/build/
