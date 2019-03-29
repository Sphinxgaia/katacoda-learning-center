## Task 1 - Basics command line

### Introduction

On the host :

`exit`{{execute T1}}
`cat /etc/os-release`{{execute T1}}
`cat /etc/hostname`{{execute T1}}


> Ensure you have docker installed before run these commands

Docker use a set of command to :
- Container Interaction :
  - RUN : `docker container run [OPTIONS] <container_fqdn> [CMD] [ARGS]`
    - Options :
      - -d : detached mode
      - -i : interactive
      - -t : pseudo-tty
      - -v : volume attachment
      - -u : user change
      - --rm : delete container after stop
      - more : https://docs.docker.com/engine/reference/commandline/container_run/
  - START/STOP : `docker container start/stop [OPTIONS] <container_id or container_name>`
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

Let's start our first container :
`docker container run -it sphinxgaia/training-centos:latest`{{execute T2}}

Now we are in the container, let's check OS & hostname) :

`cat /etc/os-release`{{execute T2}}
`cat /etc/hostname`{{execute T2}}

Close first terminal & Install wget package :

`yum install -y wget`{{execute T1}}

Exit the container and lunch again :

`exit`{{execute T1}}
`docker container run -it sphinxgaia/training-centos:latest`{{execute T1}}
`wget https://www.google.fr`{{execute T1}}

> Where is wget ?

`docker container ls`{{execute T1}}
`docker container ls -a`{{execute T1}}

Restart an old container :
`docker container start -a <container_id where we installed wget`{{copy}}

Then try:

`wget https://www.google.fr`{{execute T1}}