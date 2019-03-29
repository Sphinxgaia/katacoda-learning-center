## Task 4 (2/2)

### Clean

Delete all containers
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}

List your container :
- `docker container ls -a`{{execute T1}}


### Pratice next level

- `docker container run --rm -d --name stress2 --log-driver=fluentd --log-opt fluentd-address=tcp://fluentdhost:24224 --cpus 0.5 sphinxgaia/training-stress:0.1 -c 1 -i 1 -m 1 --vm-bytes 512M -t 100s -v`{{execute T2}}
- `docker container logs -f $(docker container ls -lq)`{{execute T1}}