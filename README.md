# Docker images

## Gekko-arm

Docker arm image for https://gekko.wizb.it/

Gekko github repo: https://github.com/askmike/gekko

Extra strategies github repo: https://github.com/xFFFFF/Gekko-Strategies

It can be run on a raspberry pi with docker, and docker compose installed

````
cd gekko-arm
docker compose up --build
````

Defaults on port 3000, modifie .env file to set host, port, or ssl

Running with docker but without docker compose:

````
docker run -e "HOST=192.168.1.115" -e "PORT=3000" --publish 3000:3000 danionescu/gekko-arm:latest
````


## Hometime

This is a repository that will automate the instalation of google calendar event extraction for this repo: https://github.com/veebch/hometime

````
cd hometime
docker compose up --build
````

Steps to prepare gcalcli:

Create a New Project within the Google developer console
Activate the "Create" button.
Enable the Google Calendar API
Activate the "Enable" button.
Create OAuth2 consent screen for an "UI /Desktop Application".
Fill out required App information section
Specify App name. Example: "gcalcli"
Specify User support email. Example: your@gmail.com
Fill out required Developer contact information
Specify Email addresses. Example: your@gmail.com
Activate the "Save and continue" button.
Scopes: activate the "Save and continue" button.
Test users
Add your@gmail.com
Activate the "Save and continue" button.
Create OAuth Client ID
Specify Application type: Desktop app.
Activate the "Create" button.
Grab your newly created Client ID (in the form "xxxxxxxxxxxxxxx.apps.googleusercontent.com") and Client Secret from the Credentials page.
Find out docker container id
````shell
docker ps
CONTAINER ID   IMAGE              COMMAND                CREATED              STATUS              PORTS                                               NAMES
eb819d5fc6ce   hometime-gcalcli   "apache2-foreground"   About a minute ago   Up About a minute   80/tcp, 0.0.0.0:8080->8080/tcp, :::8080->8080/tcp   hometime-gcalcli-1
````
Set gcalcli client_id and client_secret

````shell
docker exec -it eb819d5fc6ce gcalcli client-id=xxxxxxxxxxxxxxx.apps.googleusercontent.com --client-secret=xxxxxxxxxxxxxxxxx list

````
