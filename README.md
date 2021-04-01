# Traefik v2.4.8

## General feelings/overview

Pros:
- Traefik is really easy to use
- wonderful documentation
- performant

Cons:
- none that I could find

## Configuration

General stuff is configured in `traefik.yml` (or env vars, mutually exclusive). They call it "static configuration".

All routing configuration happens in what they call "Dynamic configuration". This configuration can come
from different sources, for example in this PoC I configure routes in `hello.yml` and others with Docker labels
in `docker-compose.yml`.
Allowed sources (called "providers") are configured in `traefik.yml` (static configuration).

When going to prod we'll most likely use Kubernetes resources (`Ingress`, `HTTPRoute`, `Gateway` and traefik-specific resources).

It's very easy to use, very well documented.

## Performance

Better startup performance compared to Kong

## Run the PoC

```sh
$ docker-compose up

$ echo "browse http://localhost:8080"

$ curl http://127.0.0.1/v1/hello # uses hello.yml + path matching
$ curl -H Host:hello.docker.localhost http://127.0.0.1 # uses hello.yml + host matching
$ curl -H Host:hello2.docker.localhost http://127.0.0.1 # uses Docker labels (docker-compose.yml) + host matching
```
