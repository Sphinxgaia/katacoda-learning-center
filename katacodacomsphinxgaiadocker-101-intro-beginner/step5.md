## Task 3 (2/2)

### Clean

Delete all containers
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}

List your container :
- `docker container ls -a`{{execute T1}}
- `clear`{{execute T1}}
- `clear`{{execute T2}}
- `clear`{{execute T3}}


### Pratice next level

Lunch multiple version of java for our test :
- `java -version`{{execute T1}}
- `docker container run --name version1-8 sphinxgaia/training-java:1.8`{{execute T2}}
- `docker container run --name version1-11 sphinxgaia/training-java:1.11`{{execute T3}}

Let's see our Java file :
```java
public class HelloWorld {

    public static void main(String[] args) {
        // Prints "Hello, World" to the terminal window.
        System.out.println("Hello, World");
    }
}
```

Now you will stress your VM with 2 tests :
- `htop`{{execute T1}}
- `docker container run --rm -d --name stress1 --cpus 0.5 sphinxgaia/training-stress:0.1 -c 1 -i 1 -m 1 --vm-bytes 128M -t 30s`{{execute T2}}
- `docker container run --rm -d --name stress2 --cpus 0.5 sphinxgaia/training-stress:0.1 -c 1 -i 1 -m 1 --vm-bytes 512M -t 100s`{{execute T3}}
- `docker container ls`{{execute T2}}

Lunch another stress container :
- `docker container run --rm -d --name stress2 --cpus 0.5 sphinxgaia/training-stress:0.1 -c 1 -i 1 -m 1 --vm-bytes 512M -t 100s`{{execute T3}}

Search stress pid and kill
- `kill -9 $(pidof stress)`{{copy}}
- `docker container ls -a`{{execute T2}}

Lunch another stress container and kill him :
- `docker container run --rm -d --name stress2 --cpus 0.5 sphinxgaia/training-stress:0.1 -c 1 -i 1 -m 1 --vm-bytes 512M -t 1000s`{{execute T3}}

Search stress pid and kill
- `docker container exec -it $(docker container ls -lq) bash`{{execute T3}}
- `kill 1`{{execute T3}}

Find your container :
- `docker container ls -a`{{execute T2}}

---

> You just have test container segmentation and ressources limitation.
>
> You know understand, that container process are shared ressources on host, but container offer an isolation. But process are mirrored on host and segmentation doest include kernel isolation by default.
> 
> PID 1 in container is mirror from PID of the process on the host.