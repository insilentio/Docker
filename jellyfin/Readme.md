# Docker compose file for a Jellyfin server
To be run on QNAP NAS in Container station or any other Docker compatible environment

Containers for:
- Jellyfin server

## Description

This docker compose creates the necessary containers for a Jellyfin application and exposes the internal jellyfin port (8096) on the host port 8096.

File dirs for config and cache need to be created on the host first.
File dirs for media can be configured in paragraph `volumes`.

## Run
Use `docker compose up -d` to run the application.
Use `docker compose build --pull` to update the images.

## Caveats

