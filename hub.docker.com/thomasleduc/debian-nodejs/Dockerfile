FROM debian:latest

MAINTAINER Thomas Leduc info.leducthomas@gmail.com

# update apt package repositories
RUN apt-get update

# install node.js and npm
RUN apt-get install -y nodejs npm git

# symlink node to nodejs
RUN ln /usr/bin/nodejs /usr/bin/node

# Create the code directory
RUN mkdir -p /live/api

# define Volume
VOLUME ["/live/api"]

# define working directory.
WORKDIR /live/api

# define default command.
CMD ["/bin/bash"]
