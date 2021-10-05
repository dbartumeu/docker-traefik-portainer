# Docker container management with Traefik v2 and Portainer

A configuration set-up for a Traefik v2 reverse proxy along with Portainer and Docker Compose.

This set-up makes container management & deployment a breeze and the reverse proxy allows for running multiple applications on one Docker host. Traefik will route all the incoming traffic to the appropriate docker containers and through the open-source app Portainer you can speed up software deployments, troubleshoot problems and simplify migrations.

## How to run it?

### I. Clone the repo

```
$ git clone https://github.com/dbartumeu/docker-traefik-portainer ./src
$ cd src/core
```

### II. Create credentials

Make sure your server has htpasswd installed. If it doesn’t you can do so with the following command:

```bash
sudo apt-get install apache2-utils
```

Then run the below command, replacing the `username` and `password` with the one you want to use.

```bash
echo $(htpasswd -nb <username> <password>)
```

Edit the `.env` file and add your auth string to `TRAEFIC_AUTH`. Also replace `ACME_EMAIL`, `TRAEFIC_HOST` and `PORTAINER_HOST` with your own values.

### III. Create the proxy network

```bash
docker network create proxy
```

### IV. Give the proper permissions to acme.json

```bash
sudo chmod 600 ./traefik-data/acme.json
```

### V. Run the stack

```
sudo docker-compose up -d
```
