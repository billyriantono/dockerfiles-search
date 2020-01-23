# Which base image to use
FROM debian:jessie

# Who is in charge of maintaining this image
MAINTAINER Nathan Jacobson <njacobson@fanforce.com>

# Setup environment variables
ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive

# Install system packages
RUN apt-get update && apt-get install -y \
    apt-utils \
    curl \
    dialog \
    build-essential \
    gcc \
    git-core \
    libreadline-dev \
    libssl-dev \
    libxml2-dev \
    libxslt-dev \
    libyaml-dev \
    make \
    libpq-dev
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install ruby-build
RUN git clone https://github.com/sstephenson/ruby-build.git && cd ruby-build && ./install.sh

# Install ruby and system gems
ENV CONFIGURE_OPTS --disable-install-rdoc
RUN ruby-build 2.0.0-p576 /usr/local
RUN gem install bundler
