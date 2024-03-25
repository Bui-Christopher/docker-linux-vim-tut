## Cron Job and Updates


## Custom NGINX Config
`docker run -it --rm -d -p 8080:80 --name nginx --volume ~/site-content:/usr/share/nginx/html nginx`

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
