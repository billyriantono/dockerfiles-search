# NodeJS
# Nginx
# Ruby
# Git
#
# Version       1.0

FROM amosrivera/ubuntu

MAINTAINER Amós Rivera, arivera.utpmp@gmail.org

# Update sources
RUN apt-get update

# Install package for apt-add-repository
RUN apt-get install -y software-properties-common

# Add NodeJS source
RUN add-apt-repository -y ppa:chris-lea/node.js

# Update sources
RUN apt-get update

# Install NodeJS
RUN apt-get install -y nodejs

# Install Nginx
RUN apt-get install -y nginx 

# Install Ruby
RUN apt-get install -y ruby2.0 ruby2.0-dev build-essential libssl-dev zlib1g-dev ruby-switch

# Install Git
RUN apt-get install -y git-core

# Global configuration
# RUN git config --global user.name "Amos Rivera"
# RUN git config --global user.email "arivera.utpmp@gmail.com"