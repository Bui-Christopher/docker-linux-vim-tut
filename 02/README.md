# 02 - Run Multiple Debian Containers 

## Resources
todo

## Run a Debian container
First, we'll run a debian container, and it'll be simple:

```docker run -it debian```

Once within the container, we can leave with `exit`

Let's break down the command. Of course, we first call docker, but we also have other commands. In our case we used `run`.
However, we can explore more commands with `help` Example: `docker help`.

Additionally, we have `-it`. That represents, interactive tty. It will run the default command in the Docker image, and in the case of debian, itll be `/bin/bash`

Afterward, let's check the status of the container after we exited:
```docker ps -a```

Let's clear it with something like:
```docker rm $CONTAINER_NAME```
or
```docker rm $CONTAINER_ID```

Of course, modify the placeholders with the corresponding variables on your machine.


Additional notes:
You'll notice that Docker tries to find the `debian:latest` image. If it does not exist, it'll download the image.

```Unable to find image 'debian:latest' locally```

We can see our current images with:
```docker images```

## Run a Persistant Debian container
Usually, Ubuntu/Debian or other images like Alpine are primarily used to build containers.
Thus, after running a debian container, if we exit the container, it'll automatically exit. How can we have it persist?



