# 06 - Recap and Conclusion

## 01 Recap
In this lesson, we learned what containers are, and ran our first `hello world`!
## 02 Recap
We explored running debian containers and tested commands and options. For example:
1. `-it`: Interactive
2. `-d`: Detached
3. `ps`: Show running containers
4. `stop`: Stop a container
5. `rm`: Remove a container
6. `namr`: Name a container
6. `exec`: Execute into the container's tty
## 03 Recap
Introduction to basic Linux commands and NeoVim
1. `mkdir`: Make a directory
2. `rmdir`: Remove a directory
3. `cd`: Change into a directory
4. `ls`: List directory contents
5. `touch`: Create a file
6. `pwd`: Print working directory
7. `apt update`: Name a container
8. `apt install`: Name a container
9. `nvim`: Name a container
## 04 Recap
This time we ran some nginx containers, praciced linux/vim commands, and explored more flags and options.
1. `-p` Exposed container ports
2. `docker logs` Logs of the container
3. `curl` We tested curling containers

We also briefly touched upon creating a bash script and running it with something like:
```
mkdir scripts
cd scripts
touch run.sh
nvim run.sh
```

Inside `run.sh`
```
#!/bin/bash
docker stop nginx && docker rm nginx
docker run -d --name nginx -p 80:80 nginx
```

Then to run it we did:
```
chmod +x run.sh
./run.sh
```
## 05 Recap
Now that we learned how to edit files and navigate the linux filesystem, we began adding volumes to our containers.
1. `--volume` Container volume
2. Dockerfiles


Overall, these lessons provide funadmental practices to Unix machines and brief overview of Docker. Good luck!
