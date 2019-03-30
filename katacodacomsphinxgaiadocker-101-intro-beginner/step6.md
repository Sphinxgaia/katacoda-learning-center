## Task 4 (1/2)

### Clean

Delete all containers
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}

List your container :
- `docker container ls -a`{{execute T1}}
- `clear`{{execute T1}}
- `clear`{{execute T2}}
- `clear`{{execute T3}}

### Introducion

By default, Docker records all stdout and stderr events on tty and then in JSON for the host (by default /var/lib/docker/containers/CONTAINER_ID/CONTAINER_ID-json.log).

You can generate events for your application, but you cannot distinguish ERR from STDOUT the error without tagging on your part.

### Pratice

Lunch container and find its logs :
- `docker container run --rm -d --name stress1 --cpus 0.5 sphinxgaia/training-stress:0.1 -c 1 -i 1 -m 1 --vm-bytes 128M -t 30s`{{execute T2}}
- `ls -al /var/lib/docker/containers/`{{execute T1}}
- `tail -f /var/lib/docker/containers/CONTAINER_ID/CONTAINER_ID-json.log`{{copy}}

> You see your container logs.

Another test :
- `docker container run -it sphinxgaia/training-centos:latest`{{execute T2}}
- `ls -al /var/lib/docker/containers/`{{execute T1}}

On terminal 1, tail logs your last container
- `tail -f /var/lib/docker/containers/CONTAINER_ID/CONTAINER_ID-json.log`{{copy}}

Run some command in you container on terminal 2 :
- what do you observe in terminal 1 ?