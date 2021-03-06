## Task 1 (3/4)

### Clean

- `docker container ls -a`{{execute T1}}

Delete all
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}
- `clear`{{execute T1}}

### Introduction level 3

Using Dockerfile to build a container is the first step in automation with Docker. It's a good tip when your debt is null.

If my debt isn't null ?

I have to use product or process to capitalize between legacy and container.

Let's see Ansible and Packer. Packer is a tool to process template and produce an output image for different environment (AWS, Container, VMWARE, ...).

The combination of Ansible (also used for legacy purposes) and Packer (multi env builder) allows us to build containers with less effort.

### Pratice next level

- Create a directory for our build :
  - `cd ~ && mkdir packer && cd packer`{{execute T1}}
- Install Packer and Ansible :
  - `wget https://releases.hashicorp.com/packer/1.3.5/packer_1.3.5_linux_amd64.zip && unzip packer_1.3.5_linux_amd64.zip`{{execute T1}}
  - `mv packer /usr/local/bin`{{execute T1}}
  - `pip install ansible`{{execute T1}} 

Then clone demo repo :
- `git clone https://github.com/Sphinxgaia/training-packer-docker-ansible-demo.git && cd training-packer-docker-ansible-demo`{{execute T1}}
- `packer build java.json`{{execute T1}}
- `docker container run -it sphinxgaia/centos:v1.2`{{execute T1}}

Let's analyze your image :
- `dive sphinxgaia/centos:v1.2`{{execute T1}}

> Now you're able to install Java 11 on CentOS container as CentOS hosts (VM, Baremetal, ...)


--- 

> Packer is an interesting tool to use your Ansible's playbook with the standardization of the construction of your docker image, AMI AWS or other image.
> 
> Here we use a simple playbook and export the result to a docker image.
> 
> There is a lot of solutions to build docker image. We use the most simple with Dockerfile compatible method with :
> - `docker image build` command
> - buildah or podman (redhat alternative to docker)
> - kaniko : docker image builder in Kubernetes
> - JIB : builder for with mvn like image
> - bazel : complex layer construction without docker