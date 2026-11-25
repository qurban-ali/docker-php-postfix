# docker-php-fpm-nginx-postfix
## Introduction
This is a repository that can be used to run php, php-fpm, nginx, postfix on docker / kubernetes. This can be used as a dev environment for developer as well as a base docker image to build other images on top of.
## Versioning
* 1.0.x for php7
* 1.1.8 for php8
## How to use this
### Changes required to make postfix work
* Make changes to the postfix/sasl_passwd file and update it with your own smtp details
* Make changes to the postfix/main.cf file and update the following lines
    sender_canonical_maps = static:no-reply@nodesol.com
    relayhost = smtp.nodesol.com:587
### Building with docker
    docker build -t nodesol-base:latest .
### Running a docker container for code development
    docker run -d -p 127.0.0.1:8000:80 --name=nodesol-base -v "$(pwd):/home/nodesol/public" nodesol-base:latest

Run this from a directory containing only files intended to be served by Nginx (for Laravel, use the application's public directory, or adapt the container layout). Open http://localhost:8000 to access the local server.

### Security and maintenance

The Dockerfile copies the SMTP password file into the image. Do not commit real SMTP credentials or publish images built with them; use a runtime secret mechanism before deploying. This image uses Alpine 3.13 and PHP 8 packages from an old release. Treat it as a legacy development example, not a production-ready image.
