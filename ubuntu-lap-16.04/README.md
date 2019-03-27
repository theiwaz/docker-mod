ubuntu-lap
======================

Dockerfile for base Apache + PHP image

Based on Ubuntu 16.04 Xenial and PHP 7.0 (no extra extensions)

Usage
-----

To create the image `registry.mindef.nl/docker/ubuntu-lap`, execute the following command on the docker-cakephp directory:

```bash
docker build -t registry.mindef.nl/docker/ubuntu-lap:latest .
```

Optional: You can now push your new image to a registry:

```bash
docker push registry.mindef.nl/docker/ubuntu-lap
```

Running your LAP docker image
-----------------------------------

Start your image forwarding container port 80 to localhost port 80:

```bash
docker run -d -p 80:80 registry.mindef.nl/docker/ubuntu-lap
```
