# Docker CLI CheatSheet

## Create, validate and manage docker images:
Download an image from [DockerHub](https://hub.docker.com/) and will be stored locally under
`/var/lib/docker/*` after processing from Docker-Engine. Docker pull takes via default always the latest-tag, except you defined something else.:
```
docker pull <image-name:tag>
```

Remove one or more images from local Docker repository and from `/var/lib/docker/*`:
```
docker rmi <image-id or image-name>
```

Delete all local images at once:
```
docker rmi $(docker images -q)
```

Remove dangling images (images with `none:none --> REPOSITORY:TAG`):
```
docker image prune
```

This allows us to retrieve extended (meta) information about locally stored images. Meta information includes e.g. the complete ID of the image, tags, from which base image the existing image was image was derived from, the creation date, comments, build host, environment variables, the start command, the vendor and many more. But we can't find out anything about binaries, libraries and tools used in it:
```
docker image inspect <image-id or image-name>
```
---
## Manage and operate container instances:
Create a Centos container in interactive session:
```
docker container run --name=mycontainer -ti centos:latest
```

Create a container in detached session (default). If no --name=<container-instance-name> is specified, Docker chooses a two-part, underscore-separated random name for the container (e.g. blue_wall):
```
docker run --name=nginx -d nginx:latest
```

List all running container:
```
docker ps
```

List all container:
```
docker ps -a
```

List latest running container:
```
docker ps -l
```

Stop a running container:
```
docker stop <container-id or name>
```

Start an available stopped container:
```
docker start <container-id or name>
```

Restarts a running container. With `-t` you can specify a maximum timeout:
```
docker restart <container-id or name>
```

Remove a stopped container instance (incl. ReadWrite layer):
```
docker rm <container-id or name>
```

Force delete without stopping first:
```
docker rm -f  <container-id or name>
```

See the history of ngx container to export this running container:
```
docker image history nginx
```

Export a stopped container (e.g. nginx) to an image:
```
docker container export ngx > co7_export.tar; ls -la co7_export.tar
```

Show an overview of the running processes inside the container:
```
docker top <container-id or name>
```

---
## Reference
[Docker CLI Docs](https://docs.docker.com/engine/reference/commandline/cli/)