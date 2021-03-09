# Docker images

## Gekko-arm

Docker arm image for https://gekko.wizb.it/

Gekko github repo: https://github.com/askmike/gekko

Extra strategies github repo: https://github.com/xFFFFF/Gekko-Strategies

It can be run on a raspberry pi with docker, and docker compose installed

````
cd gekko-arm
docker-compose build
docker-compose up
````

Defaults on port 3000, modifie .env file to set host, port, or ssl

Running with docker but without docker compose:

````
docker run -e "HOST=192.168.1.115" -e "PORT=3000" --publish 3000:3000 danionescu/gekko-arm:latest
````