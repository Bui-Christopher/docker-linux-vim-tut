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

```
mkdir docker
touch Dockerfile
nvim Dockerfile
```

```todo```
