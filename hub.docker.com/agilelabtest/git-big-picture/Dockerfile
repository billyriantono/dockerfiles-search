FROM ubuntu:17.10
MAINTAINER Bruno Delb "brunodelb@gmail.com"

RUN apt-get update

# Install Python
RUN \
  apt-get install -y python python-dev python-pip python-virtualenv && \
  rm -rf /var/lib/apt/lists/*

# Install git
RUN apt-get update && apt-get install -y git

RUN apt-get install -y graphviz

WORKDIR /data
# RUN wget https://raw.github.com/esc/git-big-picture/master/git-big-picture

COPY ./git-big-picture /usr/bin/git-big-picture
RUN chmod +x /usr/bin/git-big-picture
# CMD git-big-picture -o graph.png
