# Docker images

## Gekko-arm

Docker arm image for https://gekko.wizb.it/

It can be run on a raspberry pi with docker, and docker compose installer

````
cd gekko-arm
docker-compose build
docker-compose up
````

Defaults on port 3000, modifie .env file to set host, port, or ssl
