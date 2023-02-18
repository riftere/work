# Stored in /usr/local/searxng-docker
searxng-docker
Create a new SearXNG instance in five minutes using Docker

What is included ?
Name	Description	Docker image	Dockerfile
Caddy	Reverse proxy (create a LetsEncrypt certificate automatically)	caddy/caddy:2-alpine	Dockerfile
SearXNG	SearXNG by itself	searxng/searxng:latest	Dockerfile
Redis	In-memory database	redis:alpine	Dockerfile-alpine.template
How to use it
Install docker
Install docker-compose (be sure that docker-compose version is at least 1.9.0)
Get searxng-docker
cd /usr/local
git clone https://github.com/searxng/searxng-docker.git
cd searxng-docker
Edit the .env file to set the hostname and an email
Generate the secret key sed -i "s|ultrasecretkey|$(openssl rand -hex 32)|g" searxng/settings.yml
Edit the searxng/settings.yml file according to your need
Check everything is working: docker-compose up
Run SearXNG in the background: docker-compose up -d
How to access the logs
To access the logs from all the containers use: docker-compose logs -f.

To access the logs of one specific container:

Caddy: docker-compose logs -f caddy
SearXNG: docker-compose logs -f searxng
Redis: docker-compose logs -f redis
Start SearXNG with systemd
You can skip this step if you don't use systemd.

cp searxng-docker.service.template searxng-docker.service
edit the content of WorkingDirectory in the searxng-docker.service file (only if the installation path is different from /usr/local/searxng-docker)
Install the systemd unit:
systemctl enable $(pwd)/searxng-docker.service
systemctl start searxng-docker.service
Note on the image proxy feature
The SearXNG image proxy is activated by default.

The default Content-Security-Policy allow the browser to access to ${SEARXNG_HOSTNAME} and https://*.tile.openstreetmap.org;.

If some users wants to disable the image proxy, you have to modify ./Caddyfile. Replace the img-src 'self' data: https://*.tile.openstreetmap.org; by img-src * data:;.

Multi Architecture Docker images
Supported architecture:

amd64
arm64
arm/v7
How to update ?
To update the SearXNG stack:

docker-compose pull
docker-compose down
docker-compose up
To update this docker-compose.yml file:

Check out the newest version on github: searxng/searxng-docker.
