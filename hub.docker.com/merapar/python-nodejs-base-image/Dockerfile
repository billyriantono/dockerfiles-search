#
# Docker file for the creation of a base image for running python 3.5 and node 6.x applications.
#
FROM    python:3.5.3-slim

MAINTAINER Merapar

RUN     apt-get update && apt-get install -y curl
RUN     curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN     apt-get install -y nodejs
