## Task 4 (2/2)

### Clean

Delete all containers
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}

List your container :
- `docker container ls -a`{{execute T1}}
- `clear`{{execute T1}}
- `clear`{{execute T2}}
- `clear`{{execute T3}}


### Pratice next level


Another test :
- `docker container run -it sphinxgaia/training-centos:latest`{{execute T2}}
- `ls -al /var/lib/docker/containers/`{{execute T1}}

On terminal 1, tail logs your last container
- `tail -f /var/lib/docker/containers/CONTAINER_ID/CONTAINER_ID-json.log`{{copy}}

Run some command in you container on terminal 2 :
- what do you observe in terminal 1 ?

Now add another process in the container :
- `docker container exec -it $(docker container ls -lq) bash`{{execute T2}}
- `ps -ef`{{execute T2}}

Run some command in you container on terminal 2 :
- what do you observe in terminal 1 ?


Docker provide the ability to log to another format and remote system, let's configure a test :
- `mkdir fluentd`{{execute T1}}
-  `echo " <source> 
   @type forward 
 </source> 
 
 <match *> 
   @type stdout 
 </match>" > fluentd/fluentd.conf`{{execute T1}}
- `docker run -it -p 24224:24224 -v /root/fluentd/:/fluentd/etc/ -e FLUENTD_CONF=fluentd.conf fluent/fluentd:latest`{{execute T2}}
- `docker container run --rm -d --name stress2 --log-driver=fluentd --log-opt fluentd-address=tcp://localhost:24224 --cpus 0.5 sphinxgaia/training-stress:0.1 -c 1 -i 1 -m 1 --vm-bytes 512M -t 100s -v`{{execute T3}}
- `docker container logs -f $(docker container ls -lq)`{{execute T1}}


Now add another process in the container :
- `docker container exec -it $(docker container ls -lq) bash`{{execute T3}}
Run some command in you container on terminal 3 :
- what do you observe in terminal 1 ?
- what do you observe in terminal 2 ?


---

> Docker container log STDOUT and STDERR on JSON format, but only the process 1 is concerned. So you have to keep this in mind.
> 
> Docker can logs after configuration to remote system or in different format. [See documentation](https://docs.docker.com/config/containers/logging/configure/) or [configuration for fluentd](https://docs.docker.com/config/containers/logging/fluentd/). A specialized scenario will be performed for the logs.