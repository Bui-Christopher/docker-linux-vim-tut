# 04 - NGINX and Intro to Bash Scripts

## Prerequisites
This lesson assumes that know how to start a debian container.
```docker run -d --name deb1 debian tail -f /dev/null```

This is a reminder of how to execute the `/bin/bash` command to hop into the debian container.
```docker exec -it deb1 /bin/bash```

It is also assumed that you can create folders, files, and write text to files.
```
mkdir scripts
touch hello.sh
nvim hello.sh
```

## Nginx
What is [Nginx](https://www.nginx.com/resources/glossary/nginx/)?

## Run an NGINX Container
Let's run our first nginx container. Many of these options should look familiar:
```
docker run --name nginx -d -p 80:80 nginx
```

1. `--name`: Name of the Container
2. `-d`: Detached mode so that we can stay on our host tty.
3. `-p $HOST_PORT:$CONTAINER_PORT`: Exposed port of the container and its relation to the host port

### Curl the Nginx container
Let's examine the container in different manners.
1. Docker Logs
    ```
    docker ps -a
    docker logs nginx
    ```
Looks like it's running, but I have no idea what these logs are saying...

2. Curl
```
curl -x GET localhost:80
```
Great. This looks a bit more readable?

3. Browser

Actually, the port `80` is a standard for browsers. When we access http://localhost, it's the same as 
entering http://localhost:80. Open up your browser (chrome, fiefox, etc) and type: `localhost`.
Hopefully, a `Welcome to nginx!` page appears.

Let's try our nginx container again but different ports.
```
docker stop nginx && docker rm nginx
docker run --name nginx -d -p 8080:80 nginx
docker logs nginx
curl -X GET localhost:8080
Browser: http://localhost:8080
```

## Bash Script Automation
Let's try running the container with a Bash script instead.
Let's write out our first script and run it:

Create a script named `nginx.sh` and place it within a folder: `scripts/`.

```
mkdir scripts
cd scripts
touch nginx.sh
nvim nginx.sh
```

Place this within the script:
```
#!/bin/bash
docker stop nginx && docker rm nginx
docker run -d --name nginx -p 80:80 nginx
```

Let's break down this bash script:

The first line starts with a shebang: `#!/bin/bash`. This tells the operating system what interpreter to run the script with.
In this case, we will be using `/bin/bash`. If you recall, when we hop into a container, we also call `docker exec -it $CONTAINER_NAME /bin/bash`
Afterward, we stop and remove any container with the name `nginx` and run a new `nginx` container.

Let's run this script:
`./nginx.sh`

Unfortunately, the script didn't run. Why not?
```
zsh: permission denied: ./test.sh
```

Well, it says permission denied; however, what happened is that we created a text file. Now let's convert it into an executable we can run:
```
chmod +x nginx.sh
./nginx.sh
```

Let's test it again:
```
docker logs nginx
curl -X GET localhost:80
Browser: http://localhost:80
```

## Nginx in Debian Container
So far, we've worked with running Nginx as a container. Nginx is still a software we can run on our servers, and it doens't have to be dockerized.
Thus, let's try it with a linux container! Let's try an ubuntu container this time.

```
docker run -d --name deb -p 80:80 ubuntu tail -f /dev/null
docker exec -it ubuntu /bin/bash
apt update
apt install nginx -y
nginx
nginx -t
exit
```

Since this container is exposed, let's test it like we did previously:
```
docker logs nginx
curl -X GET localhost:80
Browser: http://localhost:80
```
