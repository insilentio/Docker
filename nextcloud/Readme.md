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

Use `docker compose up -d` to run the application. Change to the nextcloud *url:port* and start the installation by choosing an admin user name and pw.
Use `docker compose build --pull` to update the images. A manual build update ma y be triggered like this: `docker build -t nc_enhanced --pull .` (e.g. for QNAP NAS, see below). Then connect to the main container `docker exec -u 33 -it <containter-id> /bin/sh` (the -u option may need to be adapted to the correct number). Run the update command for nextcloud `./occ upgrade` (ideally you are already in the correct directory, otherwise change to `cd /var/www/html`. Done.

## Caveats
Currently no healthcheck for the nextcloud container is implemented. Although something is described [here](https://github.com/nextcloud/docker/issues/676), this seems to be an uncertain solution.
This application does not use a reverse proxy.

## Note to QNAP users
It seems that Container station currently (as of QTS 5.1.4) does not support build commands in docker compose files. Hence you need to build the adapted Nextcloud image (from dockerfile) manually beforehand. Connect to your QNAP by SSH and navigate to the directory where you have downloaded the repo, then run `docker build . --tag nc_enhanced:latest`. Then create your Nextcloud application in Container station and replace the line `build: .` with `image: nc_enhanced:latest`.
Furthermore, **Make sure** to check permissions on the created volumes **before** running the nextcloud installation: the server volume must be owned and RW'ed by user `33`, the other two volumes by user `999`. Otherwise you will run into strange DB errors (like *"Base table or view not found: 1146 Table ‘nextcloud_db.oc_appconfig’ doesn’t exist"*). 
