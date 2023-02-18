# Stored in /usr/local/searxng-docker
searxng-docker

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

