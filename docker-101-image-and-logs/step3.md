## Task 1 (2/4)

### Clean

- `docker container ls -a`{{execute T1}}

Delete all
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}
- `clear`{{execute T1}}

### Introduction level 2

The Commit method is not an industrialization method. How to follow the evolution of your constructions ?

There are anothers way to build container :
- Easy way :
  - Dockerfile & Docker (request a Docker daemon)
  - Packer & Ansible (request a Docker daemon)
- Other way :
  - Buildah (no Docker daemon)
  - Jib (no Docker daemon, only Java)
  - Kaniko (request a Kubernetes Cluster)
  - ...

Dockerfile is an instruction file containing a declarative informations to build image.
- Instructions command :
  - `FROM` defined the source image (FROM scratch, FROM centos:latest)
  - `RUN` execution command(emulate a shell) : RUN yum install -y wget
  - `COPY source dest` copy file from host to image
  - `ENV` define environment variable (for container) RUN export ... only set environment variable for RUN context
  - `EXPOSE` default image port
  - `VOLUME` default volume exposition
  - `ENTRYPOINT` default command (2 mode exec or shell)
  - `CMD` args for ENTRYPOINT statement (2 mode exec or shell)

Building image doesn't support interactive mode. So all install or action must be automated.


### Pratice next level

Build from Docker command line :
- docker image build -t IMAGE_FQDN CONTEXT
- `-t` flag set the IMAGE_FQDN for the current build
- `CONTEXT` where is the Dockerfile

Write our first Dockerfile :
- Create a dir 
  - `mkdir myimage && touch myimage/Dockerfile && cd myimage`{{execute T1}}
- Then edit `myimage/Dockerfile` the file and put follow line :
  - Define base image :
    - `FROM sphinxgaia/training-centos:latest`{{copy}}
  - Installation wget
    - `RUN yum install wget`{{copy}}
  - Then Build :
    - `docker image build -t sphinxgaia/training-centos:v1.0 .`{{execute T1}}


What's wrong ? add -y to install to remove interactive install
- `RUN yum install -y wget`{{copy}}
Then rebuild image :
- `docker image build -t sphinxgaia/training-centos:v1.0 .`{{execute T1}}
Run your container :
- `docker container run -it sphinxgaia/training-centos:v1.0`{{execute T1}}
- `wget`{{execute T1}}
- `exit`{{execute T1}}
> You have an centos image with wget installed

Where is CMD and ENTRYPOINT ?
- your image is from [sphinxgaia/training-centos](https://github.com/Sphinxgaia/training-centos/blob/master/Dockerfile)

Build another version of your personnal image :
- Edit your Dockerfile and add Java 11 :
    - `ENV JAVA_VERSION=jdk-11.0.2`{{copy}}
    - `RUN wget https://download.java.net/java/GA/jdk11/9/GPL/open${JAVA_VERSION}_linux-x64_bin.tar.gz`{{copy}}
    - `RUN tar xvf open${JAVA_VERSION}_linux-x64_bin.tar.gz`{{copy}}
    - `RUN echo "
if [ \"$1\" = 'java' ]; then
  exec \"$@\"
fi >> /entrypoint.sh
"`{{copy}}
    - `
RUN mv ${JAVA_VERSION} /usr/local/ && \
echo "export JAVA_HOME=/usr/local/${JAVA_VERSION}" >> /etc/profile.d/jdk11.sh  && \
echo "export PATH=$PATH:/usr/local/${JAVA_VERSION}/bin" >> /etc/profile.d/jdk11.sh
`{{copy}}
- Change CMD (in exec mode) :
  - `CMD ["java","-version"]`{{copy}}
- Then build and run you container :
  - `docker image build -t sphinxgaia/training-centos:v1.1 .`{{execute T1}}
  - `docker container run -it sphinxgaia/training-centos:v1.1`{{execute T1}}

> You have an centos image with wget and java installed
> What you observe with during the build and layer number :
>   - `dive sphinxgaia/training-centos:v1.1`{{execute T1}} 