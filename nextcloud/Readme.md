# Docker compose file for a Nextcloud server
To be run on QNAP NAS in Container station or any other Docker compatible environment


Containers for:
- Nextcloud server
- MariaDB (SQL DB)
- Redis (Cache)
- Cron (job runner)

## Description

This docker compose creates the necessary containers for a Nextcloud application and exposes the internal SSL port (443) on the host port 5555.

Various enhancements are needed, therefore the Nextcloud image is self-built from the official nextcloud:apache image. The respective dockerfile copies three files to the container: a certificate, a private key (both needed for SSL) and a shell script file to alter respective apache settings inside the container. [Check this](https://help.nextcloud.com/t/howto-running-nextcloud-over-self-signed-https-ssl-tls-in-docker/101973) if you want to use a self signed HTTPS.

Additionally, since the Nextcloud image seems to miss a crontab and a vim command, these commands are installed  into the container.

File dirs of nextcloud, sql and redis are mapped to local file system.  
**Make sure** to replace usernames and pw's in the docker-compose.yml as well as the email in the dockerfile!

## Run
Use `docker compose up -d` to run the application.
Use `docker compose build --pull` to update the images.

## Caveats
Currently no healthcheck for the nextcloud container is implemented. Although something is described [here](https://github.com/nextcloud/docker/issues/676), this seems to be an uncertain solution.
This application does not use a reverse proxy.


