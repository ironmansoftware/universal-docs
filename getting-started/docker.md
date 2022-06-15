---
description: This page provides installation and configuration information for Docker.
---

# Docker

## Installation

Our docker image is available on [Docker Hub](https://hub.docker.com/r/ironmansoftware/universal). You can start it by pulling and then running with the default port bound.

```
docker pull ironmansoftware/universal
docker run --name 'PSU' -it -p 5000:5000 ironmansoftware/universal
```

## Persistent Data

To create a Docker image that can persist the Universal data, you can create a dockerfile like the one below.

This dockerfile exposes port 5000, creates a `/data` volume, sets configuration environment variables to store the Universal repository and database in the volume and then sets the Universal.Server as the entry point to the container.

### Linux

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
