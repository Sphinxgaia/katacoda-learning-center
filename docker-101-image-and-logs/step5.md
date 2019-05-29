## Task 1 (4/4)

### Clean

- `docker container ls -a`{{execute T1}}

Delete all
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}
- `clear`{{execute T1}}

### Introduction level 4

Docker use cache when you run container. All same layers can be shared between containers running on the same hosts.

Image is built from some immutable layers and the container uses copy-on-write mecanism.

Some of Docker actions in Dockerfile create a new layer :
- RUN
- COPY

### Pratice next level

List you image :
- `docker image ls`{{execute T1}}

Inspect both image and watch the difference (ignore Parent & Id lines) :
- `docker image inspect sphinxgaia/training-centos:latest | grep sha256`{{execute T1}}
- `docker image inspect sphinxgaia/centos:v1.2 | grep sha256`{{execute T1}}

> Docker shares layer between containers to optimize storage and cache. In the production environment, you must know the size of the cache memory and purge it if necessary.

As you see, when you run an image for the first time container download all layers as compressed archive then extract info. But more layers there are, less apps start quickly.

Launch speed test containers :
- `time docker run -it sphinxgaia/training-sleep:v0.1`{{execute T1}}
- `time docker run -it sphinxgaia/training-sleep:v0.1`{{execute T1}}
- 
Clean & Launch speed test containers :
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}
- `docker image rm sphinxgaia/training-sleep:v0.1`{{execute T1}}
- `time docker run -it sphinxgaia/training-sleep:latest`{{execute T1}}

> As you see, container take a long time to startup (~ 0m25.420s) in first use case.
> After that container uptime is near 0.636s the second time.
> >
> In the second use case, startup time is faster (~ 0m21.236s).
> After that container uptime is near 0.635s the second time.


---

> In production to accelerate and optimize container start-up and storage, the docker mechanism shares the existing identical layers between containers. But if you have too many layers, starting a new container will be less efficient because of the extraction time of all layers.