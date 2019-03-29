## Task 3 (1/2)

### Clean

Delete all containers
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}

List your container :
- `docker container ls -a`{{execute T1}}

### Introducion

> `Init` has the PID 1 on linux distribution. If you kill PID 1, your machine will hang, stop or crash. (DON'T DO THIS!!!)

A container is an isolation of processes. In a container, the process doesn't know the other one and the isolation permits to launch multiple instances or version of an app.

### Pratice

Show process on host :
- `ps -ef`{{execute T1}}
- `docker container run -it --rm --name my-container sphinxgaia/training-centos:latest`{{execute T2}}
- `ps -ef`{{execute T2}}
- `ps -ef`{{execute T1}}

Kill process bash on host with parent `containerd-shim` on terminal 1 :
```
root      5287   734  0 12:58 ?        00:00:00 containerd-shim -namespace moby -workdir /var/lib/containerd/io.containerd.runtime.v1.linux/moby/08500ef
root      5305  5287  0 12:58 pts/0    00:00:00 bash
```

> What's going on ? You loose your container in terminal 2 !
> 
> Container process is a mirrored process on host which isolation are in container. Like standard linux, kill PID kill the machine.


What happens with 2 containers :
- `docker container run -it --rm --name my-container sphinxgaia/training-centos:latest`{{execute T2}}
- `ps -ef`{{execute T2}}
- `docker container run -it --rm --name my-container2 sphinxgaia/training-centos:latest`{{execute T3}}
- `ps -ef`{{execute T3}}
- `ps -ef`{{execute T1}}
