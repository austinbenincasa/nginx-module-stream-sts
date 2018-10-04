# Docker nginx-module-stream-sts

A Docker repository to compile Alpine NGINX with 'nginx-module-stream-sts' and 'nginx-module-sts'

## Description 

Will compile Alpine Nginx Container with the following NGINX modules:

- [nginx-module-stream-sts](https://github.com/vozlt/nginx-module-stream-sts)
- [nginx-module-sts](https://github.com/vozlt/nginx-module-sts)

The core of the `Dockerfile` was taken from:

- [Docker-Nginx](https://github.com/nginxinc/docker-nginx/tree/master/mainline/alpine)

## Building

- Edit or replace the `nginx.conf` file found in the repo (will not work as-is)
- Run the following commands to build and run

```
abenincasa@computer:~/nginx-module-stream-sts$ docker build -t "nginx:stream" .
abenincasa@computer:~/nginx-module-stream-sts$ docker run -p 80:80 -p 443:443 nginx:stream
```

## NGINX Config

The current `nginx.config` file included in the repo is configured as a TCP Load Balancer.
To use the current config file for this purpose edit the server link to point to a backend server(s) and port accepting 
TCP traffic. 

To understand more about NGINX TCP/UDP Load Balancing reference: [Nginx Load Balancing](https://docs.nginx.com/nginx/admin-guide/load-balancer/tcp-udp-load-balancer/)
```
stream {
    server_traffic_status_zone;
    upstream backend {
        # change these to point to your backend servers
        server XXX.XXX.XXX.XXX:443 max_fails=3 fail_timeout=10s;
        server XXX.XXX.XXX.XXX:443 max_fails=3 fail_timeout=10s;
        server XXX.XXX.XXX.XXX:443 max_fails=3 fail_timeout=10s;
    }
    server {
        listen 443;
        proxy_pass backend;
        proxy_next_upstream on;
    }
}




```
