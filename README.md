# Overview

A quick start guide on how to start a simple load balancer with [Traefik](https://doc.traefik.io/traefik/) and Docker Compose on your local machine.



## Pre-requisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Add `127.0.0.1 hello.me` to your `hosts` file.



## Up and running


Start the `reverse-proxy` service with the following command(s):

```bash
$ git clone git@github.com:yriahi/simple-traefik-load-balancer.git
$ cd simple-traefik-load-balancer
$ docker-compose up -d reverse-proxy
```

This command pulls two images: [traefik:v2.9](https://hub.docker.com/_/traefik) and [traefik/whoami](https://hub.docker.com/r/traefik/whoami), then starts three containers in Docker Desktop:

- [Traefik](https://doc.traefik.io/traefik/): load balancer.
-  *whoami*: a simple web application that returns its hostname information with a replica of 2.

Optionally, run the command `docker ps` to verify that these containers are up and running. Now, open your browser and see Traefik's API rawdata here: http://localhost:8080/api/rawdata

[Traefik's](https://doc.traefik.io/traefik/) dashboard is available at http://localhost:8080/

### Verify the load balancing


Open your web browser, and visit http://hello.me/. You will now see e.g. `Hostname: abc1234567890`. Stop the second running container of the whoami app. After your refresh your browser, you will now get a different hostname.

🎊 Now, we are successfully running a local simple load balancer with [Traefik](https://doc.traefik.io/traefik/) within our Docker Desktop environment.



## Helpful commands

Let's scale up the *whoami* "application" to run with two containers by running the following command: 

```bash 
$ docker-compose up -d --scale whoami=4
```



## Sources:

- https://doc.traefik.io/traefik/
- https://github.com/traefik/traefik
- https://hub.docker.com/_/traefik
