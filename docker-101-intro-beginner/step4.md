## Task 3 (1/2)

### Clean

Delete all containers
- In `Terminal 1`
  - `docker container rm -f $(docker container ls -aq)`{{execute T1}}

List your container :
- In `Terminal 1`
  - `docker container ls -a`{{execute T1}}
  - `clear`{{execute T1}}
- In `Terminal 2`
  - `clear`{{execute T2}}

### Introducion

> `Init` has the PID 1 on linux distribution. If you kill PID 1, your machine will hang, stop or crash. (DON'T DO THIS!!!)

A container is an isolation of processes. In a container, the process doesn't know the other one and the isolation permits to launch multiple instances or version of an app.

### Pratice

Show process on host :
- In `Terminal 1`
  - `ps -ef`{{execute T1}}
- In `Terminal 2`
  - `docker container run -it --rm --name my-container sphinxgaia/training-centos:latest`{{execute T2}}
  - `ps -ef`{{execute T2}}
- In `Terminal 1`
  - `ps -ef`{{execute T1}}

Kill process bash on host with parent `containerd-shim` in terminal 1 :
```
root      5287   734  0 12:58 ?        00:00:00 containerd-shim -namespace moby -workdir /var/lib/containerd/io.containerd.runtime.v1.linux/moby/08500ef
root      5305  5287  0 12:58 pts/0    00:00:00 bash
```

> What's going on ? You loose your container in terminal 2 !
> 
> Container process is a mirrored process on host which isolation are in container. Like standard linux, kill PID kill the machine.


What happens with another container :
- In `Terminal 2`
  - `ps -ef`{{execute T2}}
- In `Terminal 3`, if not present it will appear
  - `docker container run -it --rm --name my-container2 sphinxgaia/training-centos:latest`{{execute T3}}
  - `ps -ef`{{execute T3}}
- In `Terminal 1`
  - `ps -ef`{{execute T1}}


---

> In a container, all process are isolated from other container. But they are mirrored on the host (container isolation is a chroot and cgroup isolation for a process).
> 
> Kill process on the host or in the container will end the container.
> 
> /!\ Be carefull, if a container has more than 1 process, PID 1 will be the master process and will killed all other process in a container when it stops