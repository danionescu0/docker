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


## Gcalcli

This is a repository that dockerzes https://github.com/insanum/gcalcli

1) Run docker compose
````
cd gcalcli
docker compose up --build
````

Steps to prepare gcalcli:

2) Create Google project and get secrets
* Create a New Project within the Google developer console

* Activate the "Create" button.

* Enable the Google Calendar API

* Activate the "Enable" button.

* Create OAuth2 consent screen for an "UI /Desktop Application".

* Fill out required App information section

* Specify App name. Example: "gcalcli"

* Specify User support email. Example: your@gmail.com

* Fill out required Developer contact information

* Specify Email addresses. Example: your@gmail.com

* Activate the "Save and continue" button.

* Scopes: activate the "Save and continue" button.

* Test users

* Add your@gmail.com

* Activate the "Save and continue" button.

* Create OAuth Client ID

* Specify Application type: Desktop app.

* Activate the "Create" button.

* Grab your newly created Client ID (in the form "xxxxxxxxxxxxxxx.apps.googleusercontent.com") and Client Secret from the Credentials page.

3) Find out docker container id


````shell
docker ps
CONTAINER ID   IMAGE              COMMAND                CREATED              STATUS              PORTS                                               NAMES
eb819d5fc6ce   gcalcli-gcalcli   "apache2-foreground"   About a minute ago   Up About a minute   80/tcp, 0.0.0.0:8080->8080/tcp, :::8080->8080/tcp   gcalcli-gcalcli-1
````


4) Replace gcalcli client_id and client_secret below:
````shell
docker exec -it eb819d5fc6ce gcalcli --client-id=xxxxxxxxxxxxxxx.apps.googleusercontent.com --client-secret=xxxxxxxxxxxxxxxxx --noauth_local_webserver list
````

You will have an output like:
````text
Go to the following link in your browser:

    https://accounts.google.com/o/oauth2/v2/auth?client_id=873867853004-pa7hkk4b9v5bf81ute79r0o9br7n0c7d.apps.googleusercontent.com&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcalendar&access_type=offline&response_type=code
````
Enter verification code: 

5) Open the link in the browser, authenticate copy the verification code and paste it in the console, now you will be authenticated in the docker image
Now you can run commands like:
````shell
docker exec -it eb819d5fc6ce gcalcli --client-id=xxxxxxxxxxxxxxx.apps.googleusercontent.com --client-secret=xxxxxxxxxxxxxxxxx --noauth_local_webserver list
````
without authenticating again

