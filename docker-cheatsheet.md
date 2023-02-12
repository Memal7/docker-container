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

See the history of an image:
```
docker image history nginx
```

This allows us to retrieve extended (meta) information about locally stored images. Meta information includes e.g. the complete ID of the image, tags, from which base image the existing image was image was derived from, the creation date, comments, build host, environment variables, the start command, the vendor and many more. But we can't find out anything about binaries, libraries and tools used in it:
```
docker image inspect <image-id or image-name>
```

### Note: To analyse your container image even more in details and explore contents of each layer in an image, look at to this tool: [dive](https://github.com/wagoodman/dive).
---
## Manage and operate container instances:
Create a container in detached session (default). If no --name=<container-instance-name> is specified, Docker chooses a two-part, underscore-separated random name for the container (e.g. blue_wall):
```
docker run --name=nginx -d nginx:latest
```

Create a container in interactive session:
```
docker run --name=mycentos-container -it centos:latest
```

Create a container in interactive session and start bash in it:
```
docker run --name=mycentos-container -it centos:latest /bin/bash
```

List all running containers:
```
docker ps
```

List all containers:
```
docker ps -a
```

List latest running containers:
```
docker ps -l
```

Stop a running container:
```
docker stop <container-id or name>
```

Stop all containers:
```
docker stop $(docker ps -q)
```


Remove all stopped containers:
```
docker rm $(docker ps -a -q)
```

Start a stopped container:
```
docker start <container-id or name>
```

Restart a running container. With `-t` you can specify a maximum timeout:
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

Export a stopped container (e.g. nginx) to an image:
```
docker export ngx > co7_export.tar; ls -la co7_export.tar
```

Show an overview of the running processes inside the container:
```
docker top <container-id or name>
```

---
## Reference
[Docker CLI Docs](https://docs.docker.com/engine/reference/commandline/cli/)