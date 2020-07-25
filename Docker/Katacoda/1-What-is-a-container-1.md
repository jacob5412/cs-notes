# What is a container? - 1

* OS-level virtualization refers to an operating system paradigm in which the kernel allows the existence of multiple isolated user space instances.
* Such instances, called containers may look like real computers from the point of view of programs running in them.
* A computer program running on an ordinary operating system can see all resources (connected devices, files and folders, network shares, CPU power, quantifiable hardware capabilities) of that computer.
* However, programs running inside of a container can only see the container's contents and devices assigned to the container.

## Processes

Containers are just normal Linux Processes with additional configuration applied. 

Launching a redis container:

```bash
$ docker run -d --name=db redis:alpine
Unable to find image 'redis:alpine' locally
alpine: Pulling from library/redis
89d9c30c1d48: Pull complete
b2eb22a0b7db: Pull complete
c5ccbdf10203: Pull complete
592c37d15428: Pull complete
b70a614994bf: Pull complete
60027bdc030c: Pull complete
Digest: sha256:ee13953704783b284c080b5b0abe4620730728054f5c19e9488d7a97ecd312c5
Status: Downloaded newer image for redis:alpine
```

* `docker run`: When an operator executes docker run, the container process that runs is isolated in that it has its own file system, its own networking, and its own isolated process tree separate from the host.

`docker ps`: command only shows running containers by default

```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
eca871e969df        redis:alpine        "docker-entrypoint.s…"   44 minutes ago      Up 44 minutes       6379/tcp            db
```

`docker top`: Display the running processes of a container, `db` is the container we're using
  
```bash
$ docker top db
 PID                 USER                TIME                COMMAND
2646                999                 0:02                redis-server
```

`docker exec`: runs a new command in a running container.

```bash
$ docker exec -it db env
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=eca871e969df
TERM=xterm
REDIS_VERSION=5.0.7
REDIS_DOWNLOAD_URL=http://download.redis.io/releases/redis-5.0.7.tar.gz
REDIS_DOWNLOAD_SHA=61db74eabf6801f057fd24b590232f2f337d422280fd19486eca03be87d3a82b
HOME=/root
```

* `-i`: Keep STDIN open even if not attached
* `-t`: Allocate a pseudo-TTY. TTY is TeleTypeWriter - to print the file name of the terminal connected to standard input.

## Sources
1. [Wikipedia: OS level virtualization](https://en.wikipedia.org/wiki/OS-level_virtualization)
2. [Docker Reference](https://docs.docker.com/engine/reference/)