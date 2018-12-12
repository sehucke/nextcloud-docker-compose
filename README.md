# Build and run Nextcloud with docker-compose

## What is this?

This is a repo for building and running a Nextcloud environment with docker-compose. It is build upon scripts available in https://github.com/nextcloud/docker. It is preconfigured to run behind a Nginx reverse proxy with a Let's Encrypt companion (https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion) and an auto-generated nginx.conf (via https://github.com/jwilder/docker-gen/)

## What this repo contains

This repo contains a folder "nextcloud" with a compose file for starting the following containers:
1. `redis` - for file locking
1. `app` - the Nextcloud PHP-FPM container
1. `web` - a Nginx container for serving static files and pass-through to `app`
1. `cron` - another instance of the Nextcloud PHP-FPM container, but with a different entry point for performing the cron tasks

The images for `app/cron` and `web` need to be built by calling `docker-compose build --pull`. The `Dockerfile`s and configs reside in the corresponding subfolders.

The database resides in a separate compose file in the folder "mariadb". You can also think about integrating it into Nextcloud's compose file to have a single file for the whole service.

## How to use this?

First, set up a reverse proxy. Then...

1. Clone this repo.
2. Add your configuration where needed (`env`vars/files, custom PHP and MariaDB parameters depending on your environment).
3. Run `docker-compose up -d`.
