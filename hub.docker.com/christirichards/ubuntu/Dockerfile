FROM ubuntu:16.04
MAINTAINER christi@christirichards.com

# Install tools software
RUN echo 'APT::Install-Recommends 0;' >> /etc/apt/apt.conf.d/01norecommends \
 && echo 'APT::Install-Suggests 0;' >> /etc/apt/apt.conf.d/01norecommends \
 && apt-get update -qq \
 && apt-get install -qqy \
    vim.tiny \
    curl \
    wget \
    net-tools \
    ca-certificates \
    unzip

# Clean
RUN rm -rf /var/lib/apt/lists/*
