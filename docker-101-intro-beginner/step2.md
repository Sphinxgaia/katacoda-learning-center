## Task 1 (1/2)

### Introduction

> Ensure you have docker installed before run these commands

Docker use a set of command to :
- Container Interaction :
  - RUN : `docker container run [OPTIONS] <IMAGE_FQDN> [CMD] [ARGS]`
    - IMAGE_FQDN : we will see this in futur scenario
    - Options :
      - -d : detached mode
      - -i : interactive
      - -t : pseudo-tty
      - -v : volume attachment
      - -u : user change
      - --rm : delete container after stop
      - more : https://docs.docker.com/engine/reference/commandline/container_run/
  - START/STOP : `docker container start/stop [OPTIONS] <CONTAINER_ID or CONTAINER_NAME>`
    - START OPTIONS :
      - -a : attach container shell to tty
  - List : `docker container ls [OPTIONS]`
    - -a : all (run or stopped container)
    - -q : only container id
- Image Interaction :
  - List : `docker image ls`
- Volume Interaction
- Network Interaction 

### Pratice

On the host :
- `cat /etc/os-release`{{execute T1}}
- `cat /etc/hostname`{{execute T1}}


Let's start our first container :
- `docker container run -it sphinxgaia/training-centos:latest`{{execute T1}}


Now we are in the container, let's check OS & hostname) :
- `cat /etc/os-release`{{execute T1}}
- `cat /etc/hostname`{{execute T1}}


Install wget package :
- `yum install -y wget`{{execute T1}}


Exit the container and launch again :
- `exit`{{execute T1}}
- `docker container run -it sphinxgaia/training-centos:latest`{{execute T1}}
- `wget https://www.google.fr`{{execute T1}}

> Where is wget ?
- `exit`{{execute T1}}
- `docker container ls`{{execute T1}}
- `docker container ls -a`{{execute T1}}

Restart an old container :
- `docker container start -a <container_id where we installed wget>`{{copy}}

Then try:
- `wget https://www.google.fr`{{execute T1}}
- `exit`{{execute T1}}


---

As you see, the container :
- hostname is an hexadecimal name (if you pay attention, it is the container id when you execute a `docker container ls`)
- `docker container run` command instantiate a new container on every execution