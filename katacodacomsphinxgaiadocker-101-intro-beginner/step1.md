Docker is a greate tool to do container more easier than before. But what is a container ? Why use this ?

## Container vs Virtual Machine

Virtual Machine has a guest OS with all bin, libs and stuff provides by Linux distribution (some linux distributions : CentOS, RedHat, Ubuntu, Fedora, Alpine, ...).
It isolates  vCPU / RAM guaranteed or shared to the virtual machine and do some isolation between the others virtuals machines on the host (a.k.a. VMWARE).

The minimum recommanded disk for `CentOS is about 10 GB`.
The difficulty is when you have to migrate your development to production. You can't deploy a snapshot of your VM because your Dev environment isn't the same about your PROD.

Containers were born long before Docker but Docker give simple and shorts commands to instantiate an isolation of process running inside the Container.
Isolations are based on cgroup, Kernel capabilities, ...

Container are lighter than VM (`CentOS is about 200 MB`).

A container is an instantiation of an immutable image (deep explaination in a futur scenario). So Dev environment could easily send in Prod and both ar iso


Language & Comparison Container vs VM :

| VM | vs | Container |
|:---:|:---:|:---:|
| v | **CPU isolation** | ~ |
| v | **RAM isolation** | ~ |
| 10s -> 10 min | **Boot time** | ~1s |
| 1 - 2 hours (without entreprise process) | **Build speed** | 10min |
| x | **ISO Prod** | v |
| 10 GB | **Size** | 200 MB |


## Task 1 - Basics command line

Docker use a set of command to :
- RUN : `docker container run <container_fqdn>`
- START/STOP : `docker container start/stop <container_id or container_name>`

Let's start our first container :
`docker container run -it sphinxgaia/training-centos:latest`{{execute T1}}

Now we are in a container (Terminal 1) :

`cat /etc/os-release`{{execute T1}}
`cat /etc/hostname`{{execute T1}}

On the host :

`exit`{{execute T1}}
`cat /etc/os-release`{{execute T1}}
`cat /etc/hostname`{{execute T1}}