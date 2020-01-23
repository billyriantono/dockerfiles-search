# Use phusion/baseimage as base image. To make your builds
# reproducible, make sure you lock down to a specific version, not
# to `latest`! See
# https://github.com/phusion/baseimage-docker/blob/master/Changelog.md
# for a list of version numbers.
FROM phusion/baseimage:0.9.22
MAINTAINER David Perez <davidpv@gmail.com>
CMD ["/sbin/my_init"]

RUN echo 'export PATH=$PATH:/usr/local/bin' >> $HOME/.bashrc
RUN apt-get update && apt-get install -y curl gnupg2 && curl -sL https://deb.nodesource.com/setup_6.x | bash - && apt-get install -y nodejs build-essential
RUN npm install -g @angular/cli
RUN npm install -g cordova
RUN npm install -g ionic
RUN npm install -g typescript

WORKDIR /home/root/project
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 8100


