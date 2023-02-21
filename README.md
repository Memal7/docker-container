# Containerization of a 3-tier application with Docker

This repo demonstrates containerization of a 3-tier node.js application with Docker and Docker-Compose.

In addition the [Cheatsheet](docker-cheatsheet.md) explains some fundamental aspects of Docker containers such as create and manage container images and how to create, manage, and operate container instances.

---

## Pre-requisites

Docker (e.g. [Docker Desktop](https://www.docker.com/products/docker-desktop/))

---

## Quick Start

To build all 3 containers at once from [docker-compose.yml](./docker-compose.yml), run the following command:

```
docker-compose up
```

Otherwise, start with the [Cheatsheet](docker-cheatsheet.md) first and try to understand what each command does. Then look at the Dockerfiles in [api folder](./api/) and [client folder](./client/) and also understand what each instruction does in the Dockerfiles.

---
## Reference

- [Docker CLI](https://docs.docker.com/engine/reference/commandline/cli/)
- [Container-Golang - Containers from scratch in Go](https://github.com/Memal7/container-golang)
