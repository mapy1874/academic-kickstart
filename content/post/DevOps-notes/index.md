---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "DevOps Notes"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-06-09T17:13:57-04:00
lastmod: 2020-06-09T17:13:57-04:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## Docker

### 1. Use Docker Images

Run a container from a image. Execute this command for multiple times will generate several different containers from the same image.

```bash
docker run <image>
```

Lists the containers that are **still running**. Add the `-a` switch in order to see containers that **have stopped**.

```bash
docker ps
```

Retrieves the logs of a container, even when it has stopped

```bash
docker logs <id>
```

See the most recent 10 seconds of logs for our running container:

```bash
docker logs --since 10s <id>
```

Gets detailed information about a running or stopped container

```bash
docker inspect <id>
```

Stop a container that is still running

```bash
docker stop <id>
```

Deletes a container

```bash
docekr rm <id>
```

Deletes all stopped container

```bash
docker container prune -f
```

Let my machine to listen for incoming connections on port 8085 and route them to port 80 inside a container that runs NGINX.

 `-d` is meant to disconnect while allowing the long-lived container to continue running in the background. Running a container as detached means that you immediately get your command-line back and the standard output from the container is not redirected to your command-line anymore.

```bash
docker run -d -p 8085:80 nginx
```

Use volumes

When the container dies (the host machine restarts, the container is moved from one node to another in a cluster, it simply fails, etc.) all of that data is lost. Using a volume, you map a directory inside the container to a persistent storage. 

```dockerfile
docker run -v /your/dir:/var/lib/mysql -d mysql:5.7
```

List the local images:

```bash
docker image ls
```



### 2. Create Docker Image

Two basic components: A Docker image is created using the *docker build* command and a *Dockerfile* file.

#### Dockerfile Instructions

FROM: A *Dockerfile* file always begins with a *FROM* instruction because every image is based on another base image. 

```dockerfile
FROM node:11-alpine
```

> Don’t use latest! First of all, it doesn’t mean that any running container will be based on the latest available version of the *nginx* image. Docker is about having reproducible images, so the *latest* version is evaluated when you build your image, not when the container is run. This means that the version will not change unless you run the *docker build* command again.

COPY: Useful when I want files to be part of an image I create. Its first parameter is the file to be copied from the build context and its second parameter is the destination directory inside the image.

```dockerfile
COPY index.html /usr/share/nginx/html
```

CMD: The *CMD* instruction specifies which executable is run when a container is created using your image and provides optional arguments.

Both the program to run and its arguments are provided as a JSON array of strings.

```dockerfile
CMD ["echo", "Hello world"]
```

ENV: Define a default value for an environment variable, in case it isn’t provided when a container is created; this may be done in the *Dockerfile* file, using the *ENV* instruction.

```dockerfile
ENV radius=20
```

The environment variables can be access in shell by $radius, in Node.JS by process.env.name

VOLUME: store your data in a persistent file system.

```dockerfile
VOLUME /path/to/directory
```

The */path/to/directory* is a path to a directory used inside the image. When a container is created using the *docker run* command, the *-v* switch can be used to map this directory to an actual volume on the host system.

> Caveat: It’s best not to think about containers as long-lived, even when they are. Don’t store information inside the containers. In other words, ensure your containers are stateless, not stateful. A stateless container never stores its state when it is run while stateful containers store some information about their state each time they are run. We’ll see later on how and where to store your container’s state. Docker containers are very stable, but the reason for having stateless containers is that this allows for easy scaling up and recovery. More about that later.

EXPOSE: Purely for documentation purposes. It enables someone who wants to run a container from your image to know which ports they should redirect to the outside world using the *-p* switch of the *docker run* command.

Listen to TCP port 80:

```dockerfile
EXPOSE 80
```



#### Build command

Build the dockerfile in current directory and name the image as `<name>`

```bash
docker build -t <name> .
```

Run a container from the image created (i.e. `hello`).

 `--rm` let docker trash the created container after execution.

```bash
docker run --rm hello
```

`-it` allows the user to stop the container using Ctrl-C from the command-line

```bash
docker run --rm -it -p 8082:80 webserver
```



### 3. Publish Docker Images

A three-step process:

1. Build your image (*docker build*) with the appropriate prefix name or tag (*docker tag*) an existing one appropriately.

   For a image in the current directory that is not built yet:

   ```bash
   docker build -t <username>/<name>:<tag> .
   ```

   For an existing image:

   ```bash
   docker tag <name> <username>/<name>:<tag>
   ```

2. Log into the Registry (*docker login*).

   ```bash
   docker login -u <username> -p <password>
   ```

3. Push the image into the Registry (*docker push*).

   ```bash
   docker push <username>/<name>:<tag>
   ```

Private registries: A private registry ensures that only you can access your private images, while a public registry allows you to make your private images public for selective parties.

Which list of factors influences the size of an image?

- The files included in your image

  1. Avoid `COPY` instructions that are too broad like `COPY . .`
  2. Use *.dockerignore* to exclude files that should be excluded from the build

- The base image size

  1. `debian:8-slim` is smaller than `debian:8`, `nginx:1.15-alpine` is smaller than `nginx:1.15`

- Image layers

  1. In a future build, Docker will use the cached part instead of recreating it as long as it is possible.

  2. When pushing a new version of the image to a Registry, the common part is not pushed.

  3. When pulling an image from a registry, the common part you already have is not pulled.

     The following *docekrfile* places `COPY` instruction at the very end as this is then instruction that will change a lot. If putting `COPY` right after `FROM`, the `RUN` instruction will also need to be pushed or pulled in this case.

     ```bash
     FROM debian:8
     
     RUN apt-get update && apt-get upgrade && apt-get dist-upgrade -y
     RUN apt-get install -y php5
     
     COPY . .
     ```

     

