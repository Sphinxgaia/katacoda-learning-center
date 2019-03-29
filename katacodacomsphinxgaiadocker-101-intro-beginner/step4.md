## Task 2 - Container Isolation

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