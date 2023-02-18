# Docker CLI CheatSheet

## Create, validate and manage docker images

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

## Manage and operate container instances

Create a container in detached session (default). If no --name=<container-instance-name> is specified, Docker chooses a two-part, underscore-separated random name for the container (e.g. blue_wall):
```
docker run -d --name=nginx nginx:latest
```

Create a container in interactive session:
```
docker run -it --name=mycentos-container centos:latest
```

Create a container in interactive session and start bash in it:
```
docker run -it --name=mycentos-container centos:latest /bin/bash
```

Create a container in interactive session with automatically delete option after exiting bash:
```
docker run -it --rm --name=mycentos-container centos:latest /bin/bash
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

Display container logs:
```
docker logs <container-id or name>
```

Display container logs with timestamps:
```
docker logs -t <container-id or name>
```

Display only the last couple lines of the container logs:
```
docker logs --tail <container-id or name>
```

Display container resource usage:
```
docker stats <container-id or name>
```

Constraint container memory usage to a given amount (`-m` or `--memory`):
```
docker run -d --name mycontainer -m="200m" nginx
```

Constraint container CPU usage to a given amount (`-c` or `--cpu`):
```
docker run -d --name mycontainer --cpus="1.5" nginx
```

Constraint container CPU cores (e.g. "0-2" means to use the first, second, and third CPU):
```
docker run -d --name mycontainer --cpuset-cpus="0-2" nginx
```

Set an environment variable (`-e` or `--env`):
```
docker run -d --name postgresDB -e POSTGRES_PASSWORD=secretpa$$ postgres
```

---

### Docker Volume

Display all volumes:
```
docker volumes ls
```

Create a volume: 
```
docker volume create myVolume
```

Inspect a volume:
```
docker volume inspect myVolume
```

Delete a volume:
```
docker volume rm myVolume
```

Create a container with automatically delete option and mount it to a volume (test-folder going to be created automatically):
```
docker run -it --rm --name=mycentos-container -v myVolume:/test-folder centos:latest /bin/bash 
```

Within the container first move the test-folder inside the volume, then create a test-file:
```
cd test-folder
echo "hello world container volume" > test-file.txt
ls
exit 
```

Create an another container and check, if the `test-folder/test-file` inside the volume still exits:
```
docker container run -it --rm -v myVolume:/test-folder2 alpine sh
cd test-folder2
ls
cat test-file.txt
exit
```

Create a container and mount it with a volume, but with read-only option (`ro`)):
```
docker container run -it --rm --name myubuntu -v myVolume:/test-folder3:ro ubuntu bash
```

---

## Reference

[Docker CLI Docs](https://docs.docker.com/engine/reference/commandline/cli/)