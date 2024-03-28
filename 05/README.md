# 05 - Volumes and Custom Dockerfiles

## Custom NGINX Config
Let's try to modify the initial hello world page from nginx. Create a `content/index.html` on your host machine.
This directory will be placed in the container when we run it.
```
mkdir content
cd content
touch index.html
nvim index.html
```

Place this into `index.html`:
```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Docker Nginx</title>
</head>
<body>
  <h2>Custom Nginx hello!</h2>
</body>
</html>
```

Let's run it:
```
docker run -d --name nginx -p 80:80 --volume ./content:/usr/share/nginx/html nginx
```

### Test It!
Take your pick, we have several different ways to test our new nginx config. You should see
a new page that says `Custom Nginx hello!`.
1. `docker logs nginx`
2. `curl -X GET localhost:80`
3. Browser: `http://localhost:80`

### Break Down
We should have been exposed to several of the docker options. What about the new one `--volume`?

```
-d          - Detached mode
--name      - Container name
-p          - Host/Container Ports
--volume    - Host/Container Volumes
```
If you recall from the port, it actually maps the host port to the container. Suppose we set up the ports,
 `-p 8080:80`. This sets our host port `8080` to map to the container's `80` port.

Similarily, we have a volume, `~/content`

### Examine the Container
Actually, for debugging purposes, let's examine the container. We should be able to see our custom
`index.html`.

```
docker exec -it nginx /bin/bash
ls
cd usr/share/nginx/html
ls
cat index.html
```

Ah, so the host folder we created, `content` is mapped to the container's folder `html`. While in the container,
if we created a file, would it create a file on our host machine? Let's try it.
```
docker exec -it nginx /bin/bash
cd usr/share/nginx/html
touch `test.txt`
exit
cd content
ls
```
Would you look at that? There's a file `test.txt` on our host machine!

## Custom Dockerfile
So far we've been fortunate of using dockerfiles that have pulled from dockerhub. How can we write our own docker container?
How do we create our own docker containers? With a `Dockerfile`!

### What is a Dockerfile?
[Docs](https://docs.docker.com/reference/dockerfile/)
```
A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.
```

### Create a Dockerfile
Well now that we know what a dockerfile is, let's try creating one:
```
mkdir docker
touch Dockerfile
nvim Dockerfile
```


Write this into a Dockerfile, and let's break it down.
```
# Use the official Nginx image as base
FROM nginx:latest

# Copy the HTML file to be served
COPY index.html /usr/share/nginx/html/

# Expose port 80
EXPOSE 80
```

It looks like use can use the `#` character and it'll be ignored. In this case, it'll be comments throughout the Dockerfile
to make it more human readable. Additionally, on the left, looks like commands: `FROM` `COPY` `EXPOSE`. It's a common practice
to have these commands to be in all capitals. Additionally, one of the commands copies an `index.html` into the `/usr/share/nginx/html`.
Sounds familiar?

Now that we have this Dockerfile, let's ensure that we also create that `index.html` then build the image!

```
touch index.html
nvim .index.hmtl
```

Place this into `index.html`:
```
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Docker Nginx</title>
</head>
<body>
  <h2>Custom Nginx hello!</h2>
</body>
</html>
```

Afteward, let's build and test it.
```
docker build -t custom-nginx .
docker images
```

And of course, let's run it:
```
docker run -d -p 8080:80 custom-nginx
```

Tada! We've created our own custom nginx image. We started with a preexisting image `FROM nginx:latest`. Then, we added
custom files and built the new image.
