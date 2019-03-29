## Task 3 (2/2)

### Clean

Delete all containers
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}

List your container :
- `docker container ls -a`{{execute T1}}


### Pratice next level

Lunch multiple version of java for our test :
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

There no special dependencies but we isolate and test 2 versions of Java with the same file.

[Watch file in folder java](https://github.com/Sphinxgaia/training-java/tree/1.8)
[Watch file in folder java](https://github.com/Sphinxgaia/training-java/tree/1.11)


Now you will stress your VM with 2 tests :
- `htop`{{execute T1}}
- `docker container run --rm -d --name stress1 --cpus 0.5 sphinxgaia/training-stress:0.1 -c 1 -i 1 -m 1 --vm-bytes 128M -t 30s`{{execute T2}}
- `docker container run --rm -d --name stress2 --cpus 0.5 sphinxgaia/training-stress:0.1 -c 1 -i 1 -m 1 --vm-bytes 512M -t 100s`{{execute T3}}
- `docker container ls`{{execute T2}}