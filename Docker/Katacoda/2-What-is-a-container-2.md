# What is a container? - 2

## Docker Stats

Returns a live data stream for running containers.  To limit data to one or more specific containers, specify a list of container names or ids separated by a space. You can specify a stopped container but stopped containers do not return any data.

```bash
$ docker stats db --no-stream
CONTAINER ID        NAME                CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
eca871e969df        db                  0.69%               1.422MiB / 1.952GiB   0.07%               2.56kB / 0B         69.6kB / 0B         4
```

* `--no-stream`: Disable streaming stats and only pull the first result

