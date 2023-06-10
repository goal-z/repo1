# Create webapp, create docker, push to registry & run
- Create a simple website
- base image is nginx:alpine, which is lightweight & open source webserver
- HTML website
- Dockerfile to be used to build docker image
- Image will be pushed to Docker Hub
- Will run the website locally exposing on port 80

## HTML file
```
<!DOCTYPE html>
<html>

<head>
    <title>
        Simple website
    </title>
</head>

<body>
    <h1>
        This is a simple website
    </h1>
</body>

</html>
```
## Dockerfile
```
FROM nginx:alpine
COPY index.html /use/share/nginx/html
EXPOSE 80
```
_here we are copying the html file to a location /use/share/nginx/html in the docker_
_nginx uses default html file located in the above loacation. So we are replacing that with our HTML_
