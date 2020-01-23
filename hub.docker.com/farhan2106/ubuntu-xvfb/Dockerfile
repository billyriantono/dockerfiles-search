# Set the base image
FROM ubuntu:16.04

# Dockerfile author / maintainer
MAINTAINER Name <farhan_ghazali@yahoo.com>

# Update application repository list and install the Redis server.
RUN apt update -y &&\
    apt upgrade -y &&\
    apt install default-jre -y &&\
    apt install zip unzip -y &&\
    apt install -y libx11-xcb-dev &&\
    apt install -y libgtk2.0-0 &&\
    apt install -y libxtst6 &&\
    apt install -y libxss1 &&\
    apt install -y libgconf-2-4 &&\
    apt install -y libnss3-dev &&\
    apt install -y libasound2 &&\
    apt install -y xvfb
