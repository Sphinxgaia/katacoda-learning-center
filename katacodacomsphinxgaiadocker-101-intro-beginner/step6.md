## Task 4 (1/2)

### Clean

Delete all containers
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}

List your container :
- `docker container ls -a`{{execute T1}}

### Introducion

By default, Docker records all stdout and stderr events on tty and then in JSON for the host (by default /var/lib/docker/containers/<onctainer_id>/<onctainer_id>-json.log).

You can generate events for your application, but you cannot distinguish ERR from STDOUT the error without tagging on your part.

### Pratice

