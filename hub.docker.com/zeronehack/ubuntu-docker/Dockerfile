FROM ubuntu:16.04

LABEL maintainer="darius.bualan@intechsive.com"

RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive

RUN apt-get install -y software-properties-common

RUN apt-get -y install nginx curl tmux git screen

# Install Mongodb
RUN apt-get install -y mongodb
RUN mkdir /data
RUN mkdir /data/db
RUN rm -f /var/lib/mongodb/mongod.lock
RUN mongod --repair

# Install Nodejs
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs build-essential

RUN npm install -g @angular/cli firebase-tools

# Install Neovim
RUN add-apt-repository ppa:neovim-ppa/stable
RUN apt-get update
RUN apt-get install -y neovim
RUN update-alternatives --install /usr/bin/vi vi /usr/bin/nvim 60
RUN update-alternatives --config vi
RUN update-alternatives --install /usr/bin/vim vim /usr/bin/nvim 60
RUN update-alternatives --config vim
RUN update-alternatives --install /usr/bin/editor editor /usr/bin/nvim 60
RUN update-alternatives --config editor

ENV TERM xterm-256color

VOLUME /usr/share/nginx/html
VOLUME /data/db

CMD ["bash", "-l"]
