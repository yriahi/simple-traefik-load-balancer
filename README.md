# Overview

A quick start guide on how to start a simple load balancer with [Traefik](https://doc.traefik.io/traefik/) and Docker Compose on your local machine.



## Pre-requisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)



## Up and running

### Loadbalancer with 📦 container

Start the `reverse-proxy` service with the following command(s):

```bash
$ git clone git@github.com:yriahi/simple-traefik-load-balancer.git
$ cd simple-traefik-load-balancer
$ docker-compose up -d reverse-proxy
```

This command pulls two images: [traefik:v2.9](https://hub.docker.com/_/traefik) and [traefik/whoami](https://hub.docker.com/r/traefik/whoami), then starts two containers in Docker Desktop.  [Traefik](https://doc.traefik.io/traefik/) is the load balancer, and *whoami* is a simple web application that returns its hostname information. 

Optionally, run the command `docker ps` to verify that these containers are up and running. Now, open your browser and see Traefik's API rawdata here: http://localhost:8080/api/rawdata


### Loadbalancer with 📦📦 containers

#### Two containers

Let's scale up the *whoami* "application" to run with two containers by running the following command: 

```bash 
docker-compose up -d --scale whoami=2
```

Optionally, run the command `docker ps | grep whoami` to verify that you are running two containers of the `traefik/whoami` Docker image.
```bash
ea70f8b70cc0   traefik/whoami   "/whoami"   2 minutes ago   Up 2 minutes   80/tcp   simple-traefik-load-balancer_whoami_2
1864010bfaac   traefik/whoami   "/whoami"   7 minutes ago   Up 7 minutes   80/tcp   simple-traefik-load-balancer_whoami_1
```

#### Verify the load balancing

Run the following command **<u>twice</u>**. Each time, the output will show a different hostname and IP.

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

🎊 Now, we are successfully running a local simple load balancer with [Traefik](https://doc.traefik.io/traefik/) within our Docker Desktop environment.



## Sources:

- https://doc.traefik.io/traefik/
- https://github.com/traefik/traefik
- https://hub.docker.com/_/traefik
