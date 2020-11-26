---
description: This page provides installation and configuration information for Docker.
---

# Docker

## Installation

Our docker image is available on [Docker Hub](https://hub.docker.com/r/ironmansoftware/universal). You can start it by pulling and then running with the default port bound. 

```text
docker pull ironmansoftware/universal
docker run --name 'PSU' -it -p 5000:5000 ironmansoftware/universal 
```

#### Tags

| Tag | Platform |
| :--- | :--- |
| 1.3.0 | linux/amd64 |
| 1.3.0-windowsservercore-1909 | windows/amd64 |

## Persistent Data

To create a Docker image that can persist the Universal data, you can create a dockerfile like the one below. 

This dockerfile exposes port 5000, creates a `/data` volume, sets configuration environment variables to store the Universal repository and database in the volume and then sets the Universal.Server as the entry point to the container. 

### Linux

```text
FROM ironmansoftware/universal:latest
LABEL description="Universal - The ultimate platform for building web-based IT Tools" 

EXPOSE 5000
VOLUME ["/data"]
ENV Data__RepositoryPath ./data/Repository
ENV Data__ConnectionString ./data/database.db
ENV UniversalDashboard__AssetsFolder ./data/UniversalDashboard 
ENV Logging__Path ./data/logs/log.txt
ENTRYPOINT ["./home/Universal/Universal.Server"]
```

### Windows

```text
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

```text
docker build . --tag=universal-persistent
```

You can start the docker container with the run command and make sure to specify the volume to mount. 

```text
docker run --name powershelluniversal --mount source=psudata,target=/data --rm -d  -p 5000:5000/tcp universal-persistent:latest
```

