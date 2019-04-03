## Task 1 (1/4)

### Introduction

You can consider image as an template of container.

**Docker image defnition :**
A Docker image is made up of multiple layers. A user composes each Docker image to include system libraries, tools, and other files and dependencies for the executable code. Image developers can reuse static image layers for different projects. Reuse saves time, because a user does not have to create everything in an image.

### Practice

#### Create docker image

Create from other container :
- `docker container run -it sphinxgaia/training-centos:latest`{{execute T1}}
- `yum install wget`{{execute T1}}

Now exit and save the image :
- `exit`{{execute T1}}
- `docker container diff $(docker container ls -lq)`{{execute T1}}
- `docker container commit $(docker container ls -lq) sphinxgaia/training-centos:v1`{{execute T1}}

Run the new container :
- `docker container run -it sphinxgaia/training-centos:v1`{{execute T1}}
- `wget && exit`{{execute T1}}
- `docker container diff $(docker container ls -lq)`{{execute T1}}

### Analysis of image :

Install an OCI image analyzer
- `wget https://github.com/wagoodman/dive/releases/download/v0.7.1/dive_0.7.1_linux_amd64.deb`{{execute T1}}
- `apt install ./dive_0.7.1_linux_amd64.deb`{{execute T1}}

Run againt first image : 
- `dive sphinxgaia/training-centos:latest`{{execute T1}}
Quit : 
- <kbd>Ctrl</kbd>+<kbd>C</kbd>

Run againt first image : 
- `dive sphinxgaia/training-centos:v1`{{execute T1}}
Quit : 
- <kbd>Ctrl</kbd>+<kbd>C</kbd>


---

> 
> Images layers :
> 
> |  |
> |---|
> | Last layer |
> | bin/libs layer |
> | OS Layer |

> 
> Containers layers :
> 
> |  |
> |---|
> | Writeable layer |
> | Last layer |
> | bin/libs layer |
> | OS Layer |