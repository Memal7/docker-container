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

Removes dangling images (images with `none:none --> REPOSITORY:TAG`):
```
docker image prune
```

This allows us to retrieve extended (meta) information about locally stored images. Meta information includes e.g. the complete ID of the image, tags, from which base image the existing image was image was derived from, the creation date, comments, build host, environment variables, the start command, the vendor and many more. But we can't find out anything about binaries, libraries and tools used in it:
```
docker image inspect <image-id or image-name>
```
---
## Reference
[Docker CLI Docs](https://docs.docker.com/engine/reference/commandline/cli/)