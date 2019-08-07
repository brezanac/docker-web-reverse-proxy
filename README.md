# docker-amp-template

A simple HTTP/HTTPS reverse proxy, based on [Traefik](https://traefik.io/).

## Usage

### Cloning the repository ###
Clone the repository to your machine.

```
git clone https://github.com/brezanac/docker-web-reverse-proxy.git web-reverse-proxy
```

### Configuring the environmental variables file (.env) ###

Rename `.env.example` to `.env` and set a new value for `COMPOSE_PROJECT_NAME` if you need to. 

**IMPORTANT:** If you use [docker-amp-template](https://github.com/brezanac/docker-amp-template) for your project you need to preserve the default value for `COMPOSE_PROJECT_NAME` which is `web-reverse-proxy`.

### Creating a Docker network for public proxy requests ###
In order for the reverse proxy to be able to receive requests from other services (containers) you need to manually create a new Docker network.

```
docker network create web-reverse-proxy
```

Please note that you need to do this **only once**!

### Running docker-compose ###

Run Docker Compose within the newly created folder by specifying the `-d` argument, which will make the container run in the background (detached mode).

```
cd web-reverse-proxy
docker-compose up -d --build
```
**IMPORTANT:** Usually you do not need more than one instance running on the same machine because Traefik ties directly into Docker to automatically handle all the running containers.

Please note that the `proxy` service has been configured with an `unless-stopped` restart policy which means that it will continue to run until manually stopped, even after the machine has been restarted.

If you do not want the service to restart automatically you can disable that behavior by simply removing the `restart: unless-stopped` line from `docker-compose.yml`.

## Requirements

Docker 17.04.0+ or newer.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
