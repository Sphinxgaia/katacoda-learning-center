## Task 2 (2/2)

### Clean

List your container :
- `docker container ls -a`{{execute T1}}

Delete all
- `docker container rm $(docker container ls -aq)`{{execute T1}}

List your container again :
- `docker container ls -a`{{execute T1}}

List your docker images :
- `docker image ls`{{execute T1}}

### Pratice next level

Now we have a clean docker container list. We will run a container with sharefolder between host and container, exit without kill container (to not kill him) and attach container to tty.

#### Volume

Create a folder named `toto` and create `echo.txt` file :
- `mkdir toto`{{execute T1}}
- `echo "toto is my host folder" > echo.txt`{{execute T1}}
- `docker container run -it --rm -v toto:/tmp sphinxgaia/training-centos:latest`{{execute T2}}

Then edit file in container :
- `echo "toto is my container : $(cat /etc/hostname) folder too!!!!!" >> echo.txt`{{execute T2}}
- `more toto/echo.txt`{{execute T1}}
- `echo "toto is mine!!!!!" >> echo.txt`{{execute T1}}
- `more toto/echo.txt`{{execute T2}}

Volume persists after container stop
- `exit`{{execute T2}}
- `more toto/echo.txt`{{execute T1}}

#### TTY Container

List your container :
- `docker container ls`{{execute T1}}
- `docker container ls -a`{{execute T1}}

Lunch a new container :
- `docker container run -it --rm -v toto:/tmp --name my-container sphinxgaia/training-centos:latest`{{execute T2}}

Then detach :
- <kbd>Ctrl</kbd>+<kbd>P</kbd>+<kbd>Q</kbd>

List your container :
- `docker container ls`{{execute T1}}

Attach :
- `docker container attach my-container`{{execute T1}} or `docker container attach $(docker container ls -q)`{{execute T1}}

Then detach :
- <kbd>Ctrl</kbd>+<kbd>P</kbd>+<kbd>Q</kbd>

Lunch a new container & add line to text :
- `docker container run -it --rm -v toto:/tmp --name my-container2 sphinxgaia/training-centos:latest`{{execute T2}}
- `echo "toto is my container : $(cat /etc/hostname) folder too!!!!!" >> echo.txt`{{execute T2}}


#### Special volume

Lunch a new container & add line to text :
- `docker container run -it --rm -v toto:/tmp:ro --name my-container3 sphinxgaia/training-centos:latest`{{execute T2}}
- `echo "toto is my container : $(cat /etc/hostname) folder too!!!!!" >> echo.txt`{{execute T2}}
- `exit`{{execute T2}}