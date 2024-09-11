# Docker compose file for a Jellyfin server

To be run on QNAP NAS in Container station or any other Docker compatible environment

Container for:

-   Jellyfin server

## Description

This docker compose creates the necessary containers for a Jellyfin application and exposes the internal jellyfin port (8096) on the host port 8096. The additional port 8920 is reserved for https which needs additional setup work inside the server (under "Networking").

File dirs for config and cache need to be created on the host first. File dirs for media can be configured in paragraph `volumes`.

The image as of 2024-08-25 already packs necessary GPU drivers for hardware transcoding. However, the respective device (e.g. `renderD128`) must be configured in `docker-compose.yml`. Then transcoding may be set on in the jellyfin dashboard (under "Playback -\> Transcoding"). See <https://jellyfin.org/docs/general/administration/hardware-acceleration/> for details.

## Run

Use `docker compose up -d` to run the application. Use `docker compose build --pull` to update the images.

## Caveats
