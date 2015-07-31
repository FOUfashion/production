# Production Set-up

This is a Docker Compose app with all the services imported as submodules. It's configured for production usage.

## Features

- [HAProxy](http://www.haproxy.org/)
  - `frontend` and `api` are each behind a HAProxy reverse-proxy container
  - newly created containers are recognised (includes cluster discovery)
  - scaling the services is very easy: `docker-compose scale api=3 frontend=2`
- [nginx](http://nginx.org/)
  - the main reverse proxy
  - enforces HTTPS connections using HSTS
  - secure SSL certificate: 2048-bit key encrypted with SHA256
  - extra measures for security
    - `X-Frame-Options SAMEORIGIN` – block frames
    - `X-Content-Type-Options nosniff` – disable content-type sniffing
    - `X-XSS-Protection "1; mode=block"` – force enable the browser XSS filter
  - Gzip and SPDY enabled for extra speed
  - Google's [PageSpeed](https://developers.google.com/speed/pagespeed/module/?hl=en) module baked in for even more speed and performance
- [Docker](https://www.docker.com/)
  - services run inside containers using [Docker Engine](https://www.docker.com/docker-engine)
  - containers are managed with [Docker Compose](https://www.docker.com/docker-compose)
  - the cluster of servers is managed by [Docker Swarm](https://www.docker.com/docker-swarm)
  - the servers are on [Digital Ocean](https://www.digitalocean.com/) deployed with [Docker Machine](https://www.docker.com/docker-machine)

## To-Do

- set up nginx to cache static pages

## Domains

- `fou.fashion` – the frontend service
- `api.fou.fashion` – the root API endpoint
- `rethinkdb.fou.fashion` – RethinkDB dashboard
# Development Set-up

## Extra

Also do these for your own sanity:

```bash
$ alias dk=docker
$ alias dc=docker-compose
$ alias ma=docker-machine
```
