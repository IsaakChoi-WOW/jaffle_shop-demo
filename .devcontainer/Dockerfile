## Build from base Cloud Shell Image - MUST BE USED
FROM gcr.io/cloudshell-images/cloudshell:latest

## NOTES ##
# To trigger a rebuild of your Cloud Shell image:
# 1. Commit your changes locally: git commit -a
# 2. Push your changes upstream: git push origin master
# This triggers a rebuild of your image hosted at gcr.io/gcp-wow-ent-it-security-dev/devcontainer-test.
# You can find the Cloud Source Repository hosting this file at https://source.developers.google.com/p/gcp-wow-ent-it-security-dev/r/devcontainer-test

# ## Example usage
# RUN apt-get -y install lsof

## Install Python
# Which version

## Update packages from google base image
# RUN apt update && apt -y upgrade

## Install python:3.10
# RUN apt -y install python3.10

## Ensure pip is installed
# RUN apt -y install python3-pip

## Install dbt

WORKDIR /
COPY ./app/ ./

RUN python -m pip install --upgrade pip
RUN python -m pip install -r requirements.txt requirements-dev.txt
RUN dbt deps
# RUN dbt debug

RUN echo success

