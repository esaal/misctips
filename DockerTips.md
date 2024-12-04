# Docker tips
Copilot with modification, 20241128

## Build a _clean_ docker image with given tag and path
```bash
docker build --no-cache -t <image-tag> -f <Dockerfile-path> .
```
* --no-cache: Disables the use of the cache when building the image.
* -t <image-tag>: Tags the image with the specified name.
* -f <Dockerfile-path>: Specifies the path to the Dockerfile (optional if the Dockerfile is in the current directory).
* .: Indicates the build context, which is the current directory in this case.

## Example: Build docker image named "devimage" using "Dockerfile" with cache
```bash
docker build -t devimage -f Dockerfile .
```

## Create and Run container named "devcli"
### Without network:
```bash
docker run -it -v /home/<username>/GitHub:/home/dev --name devcli -d devimage:latest
```
### With network:
```bash
docker run -it -v /home/<username>/GitHub:/home/dev --network=host --name devcli -d devimage:latest
```

## Execute bash from container "devcli"
```bash
docker exec -it devcli bash
```

## Lists all running docker containers
```bash
docker ps -a
```

## Lists all docker images
```bash
docker images -a
```

## Stops all running docker containers
```bash
docker stop $(docker ps -a -q)
```

## Remove all docker containers
```bash
docker rm $(docker ps -a -q)
```

## Remove all docker images
```bash
docker rmi $(docker images -a)
```

## To delete the Docker cache and free up space on your system, you can use several commands depending on what you want to remove

### Remove Unused Data
The docker system prune command is the most comprehensive way to clean up unused data:
```bash
docker system prune -a
```
* The -a flag removes all unused images, not just dangling ones.
You will be prompted to confirm the action by typing y.

### Remove Build Cache
To specifically remove the build cache, use:
```bash
docker builder prune
```
This command removes the build cache, which can accumulate over time.
### Remove Unused Images, Containers, Volumes, and Networks
You can also remove specific types of unused Docker objects:
- Images:
```bash
docker image prune -a
```
- Containers:
```bash
docker container prune
```
- Volumes:
```bash
docker volume prune
```
- Networks:
```bash
docker network prune
```
### Remove All Unused Objects
To remove all unused objects, including images, containers, volumes, and networks, use:
```bash
docker system prune --volumes
```
This command is similar to docker system prune -a but also removes unused volumes.
