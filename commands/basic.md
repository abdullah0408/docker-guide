# 🐳 Docker – Basic Commands 

## Docker Version & Info

### Check Docker Version

Shows the installed Docker version

```bash
docker --version
```

### Docker System Information

Displays detailed information about:

- Docker Engine
- Number of images & containers
- Storage driver
- OS & kernel details

```bash
docker info
```

## Docker Images

### List Images

Shows all locally available Docker images

```bash
docker images
```

### Pull Image from Docker Hub

Downloads an image from Docker Hub

```bash
docker pull nginx
```

### Remove Image

Deletes a specific image

```bash
docker rmi image_id
```

### Remove All Images

Deletes all local images

```bash
docker rmi $(docker images -q)
```

## Docker Containers

### List Running Containers

Shows only running containers

```bash
docker ps
```

### List All Containers

Shows running + stopped containers

```bash
docker ps -a
```

### Create & Run Container (Foreground)

Runs container in foreground and attaches terminal

```bash
docker run nginx
```

→ Stops when process stops.

### Run Container in Detached Mode

Runs container in background

```bash
docker run -d nginx
```

### Run Container with Name

Assigns a custom name to container

```bash
docker run --name mynginx nginx
```

### Run Container with Port Mapping

Maps host port to container port (host:container)

```bash
docker run -p 8080:80 nginx
```

→ Access via localhost:8080

## Container Lifecycle Commands

### Stop Container

Stops a running container

```bash
docker stop container_id
```

### Start Container

Starts an existing stopped container

```bash
docker start container_id
```

### Restart Container

Stops and starts container again

```bash
docker restart container_id
```

### Remove Container

Deletes a stopped container

```bash
docker rm container_id
```

### Remove All Stopped Containers

Cleans unused containers

```bash
docker container prune
```

## Running Containers in Background & Interaction

### Run Ubuntu in Background (Keeps Alive)

```bash
docker run -dit --name myubuntu ubuntu bash
```

- `-d` → background
- `-i` → interactive
- `-t` → terminal
- `bash` → keeps container alive

### Difference: -d vs -dit

| Flag | Meaning |
|------|---------|
| `-d` | Run container in background |
| `-i` | Keep STDIN open |
| `-t` | Allocate terminal |

👉 `-dit` is best for debugging & learning  
👉 `-d` is enough for apps/services

## Execute Commands Inside Container

### Open Shell Inside Running Container

Preferred way to access container

```bash
docker exec -it container_id bash
```

If bash not available (alpine images):

```bash
docker exec -it container_id sh
```

→ exit will NOT stop the container.

## Logs & Inspect

### View Container Logs

Shows application logs

```bash
docker logs container_id
```

### Follow Logs (Live)

```bash
docker logs -f container_id
```

### Inspect Container

Shows detailed configuration, mounts, IP, env vars

```bash
docker inspect container_id
```

## Docker Build (Images)

### Build Image from Dockerfile

Creates image using Dockerfile

```bash
docker build -t myapp .
```

### Run Built Image

```bash
docker run -d -p 3000:3000 myapp
```

## Clean Up Commands (Very Important)

### Remove Unused Docker Resources

Deletes stopped containers, unused images & cache

```bash
docker system prune
```

### Remove Everything (⚠️ Dangerous)

Deletes all unused images, containers, cache

```bash
docker system prune -a
```
