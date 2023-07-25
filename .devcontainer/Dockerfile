## Start with base image of alpine linux with git installed
FROM mcr.microsoft.com/devcontainers/base:bullseye

## Install the xz-utils package
RUN apt-get update && apt-get install -y xz-utils

## Expose ports
# EXPOSE is not required for devcontainers. See 'devcontainer.json'

## Run
# CMD is not required for devcontainers. 
# Note to me: See what is used by default in this case 'docker container list'
