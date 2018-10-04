# Docker nginx-module-stream-sts

A Docker repository to compile Alpine NGINX with 'nginx-module-stream-sts' and 'nginx-module-sts'

# Description 

Will compile Alpine Nginx Container with the following NGINX modules:

- [nginx-module-stream-sts](https://github.com/vozlt/nginx-module-stream-sts)
- [nginx-module-sts](https://github.com/vozlt/nginx-module-sts)

The core of the `Dockerfile` was taken from:

- [Docker-Nginx](https://github.com/nginxinc/docker-nginx/tree/master/mainline/alpine)

# Building

- Edit or replace the `nginx.conf` file found in the repo (will not work as-is)
- Run the following commands to build and run

```
abenincasa@computer:~/nginx-module-stream-sts$ docker build -t "nginx:stream" .
abenincasa@computer:~/nginx-module-stream-sts$ docker run -p 80:80 -p 443:443 nginx:stream
```
