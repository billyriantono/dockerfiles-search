FROM ubuntu:latest
MAINTAINER Mike Mackintosh <m@zyp.io>

# Update apt
RUN apt-get update

# Install Ruby
RUN apt-get install -y curl wget git golang

# Install deps
RUN apt-get install -y \
        build-essential \
        zlib1g-dev libxml2-dev libxslt1-dev \
        git \
        awscli \
        nodejs npm

# Download and install Hugo
RUN wget https://github.com/spf13/hugo/releases/download/v0.15/hugo_0.15_amd64.deb && dpkg -i hugo_0.15_amd64.deb


# Cleanup Apt
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN npm install uglifycss -g

# Er, sure, why not
CMD ["/bin/bash"]
