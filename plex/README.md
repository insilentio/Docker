# Docker compose file for a Plex Media server

To be run on QNAP NAS in Container station or any other Docker compatible environment

Container for:
  - Plex server

## Description

See <https://hub.docker.com/r/linuxserver/plex>

This docker compose creates the necessary containers for a Plex application and exposes the internal plex port 32400 on the host port 32400.

File dirs for config need to be created on the host first. File dirs for media can be configured in paragraph `volumes`.

## Run

Use `docker compose up -d` to run the application. Use `docker compose build --pull` to update the images.
