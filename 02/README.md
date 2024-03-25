# 02 - Run Multiple Debian Containers 

## Resources
[Official Debian Docker Image](https://hub.docker.com/_/debian)

### Introduction to a Debian container
We'll run our first container!

```docker run debian```

Great, nothing happened. Let's add more commands to try and explore what actually is going on.

### Add additional flags
Let's add additional flags like "-it" and "-d"

```docker run -it debian```

Additional notes:
You'll notice that Docker tries to find the `debian:latest` image. If it does not exist, it'll download the image.

```Unable to find image 'debian:latest' locally```

We're no longer on our host terminal, and in the debian container instead! Once in the container, we can leave with `exit`

Let's break down the command. Of course, we first call docker, but we also have other commands. In our case we used `run`.
However, we can explore more commands with `help` Example: `docker --help`.

Additionally, we have `-it`. It is short hand for, "interactive" "tty". It will run the default command in the Docker image, and in the case of debian, it'll be `/bin/bash`

What happens if I remove the "-it" flag and replace it with "-d"?

```docker run -d debian```

### Container Status
Afterward, let's check the status of the container after we exited:

```docker ps```

Looks like not all the containers we have run are there. Let's try a more exhaustive search:

```docker ps -a```

Found it! We can see that it exited after we exited the tty. Let's remove it with something like:

```docker rm $CONTAINER_ID```

Using tab here will be very beneficial. type `docker rm $INITAL_CHARACTERS + TAB`

Of course, modify the placeholders with the corresponding variables on your machine.

### Add a Container Name
Let's add a name (deb) to our container instead of having docker giving the containers silly names like `sweet_ugle`

```docker run -it --name deb debian```

Now we can remove the container with its name instead of its ID.
```docker rm $CONTAINER_NAME```

### Check our installed docker images
We can see our current images with:

```docker images```

## Run a Persistent Debian container
Usually, Ubuntu/Debian or other images like Alpine are primarily used to build application containers with custom Dockerfiles.
In our case, when we run `docker run -it debian` it defaults to the `/bin/bash` command.
Thus, after running a debian container, if we exit the container, it'll automatically exit. How can we have it persist?
Well, we can force our own process to continiously run. 

```docker run -d --name deb debian tail -f /dev/null```

Let's break some of those flags down. We already have experience with `docker run -d --name deb debian` what about `tail -f /dev/null`?
Actually, this is not docker specific, rather linux specific. We're essentially calling the container to run this command. Which essentially does nothing but run a process that keeps the container running.

Check its status with:

```docker ps```

We can see the container is running, but we're still in the main VM host shell. How can we use the container's shell?
Hint: The container is running, and we now need to run a command to enter the container's tty.
What was the previous command that allowed us to run terminal commands within the previous debian containers?

`/bin/bash` was the previous command which is also the deafult command. How can we specify it? `docker help`

```docker exec -it deb /bin/bash```

Can you now run two containers?

```docker run -d --name deb1 debian tail -f /dev/null```

```docker run -d --name deb2 debian tail -f /dev/null```

