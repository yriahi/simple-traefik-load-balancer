# Overview

A simple load balancer with Traefik and Docker Compose.



## Pre-requisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)



## Up and running

### Loadbalancer with 📦 container

Start the `reverse-proxy` (service) with the following command:

```bash
$ git clone git@github.com:yriahi/simple-traefik-load-balancer.git
$ cd simple-traefik-load-balancer
$ docker-compose up -d reverse-proxy
```

This will pull two images: `traefik:v2.9` and `traefik/whoami`, then starts two containers in Docker Desktop. Optionally, run the command `docker ps` to verify that these containers are up and running. Now, open your browser and see Traefik's API rawdata here: http://localhost:8080/api/rawdata


### Loadbalancer with 📦📦 containers

#### Two containers

Let's scale up the `traefik/whoami` "application" to run with two containers by running the following command: 

```bash 
docker-compose up -d --scale whoami=2
```

Optionally, run the command `docker ps | grep whoami` to verify that you are running two containers of the `traefik/whoami` Docker image.
```bash
ea70f8b70cc0   traefik/whoami   "/whoami"                2 minutes ago   Up 2 minutes   80/tcp                                       simple-traefik-load-balancer_whoami_2
1864010bfaac   traefik/whoami   "/whoami"                7 minutes ago   Up 7 minutes   80/tcp                                       simple-traefik-load-balancer_whoami_1
```

#### Verify the load balancing

Run the following command **<u>twice</u>**. Each time, the output will show different hostnames with different IPs.

First time

```bash
$ curl -H Host:whoami.docker.localhost http://127.0.0.1
Hostname: 1864010bfaac
IP: 127.0.0.1
IP: 172.29.0.2
...
```

Second time

```bash
Hostname: ea70f8b70cc0
IP: 127.0.0.1
IP: 172.29.0.4
...
```

🎊 Now, we are successfully running a local simple load balancer with Traefik proxy within our Docker Desktop environment.



## Sources:

- https://doc.traefik.io/traefik/
- https://github.com/traefik/traefik
- https://hub.docker.com/_/traefik

