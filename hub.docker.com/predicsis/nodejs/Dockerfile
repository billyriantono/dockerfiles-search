FROM ubuntu:14.04
MAINTAINER wnkz

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get -qy dist-upgrade
RUN apt-get install -qy wget apt-transport-https
RUN apt-get update
RUN wget -qO- https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -
RUN echo 'deb https://deb.nodesource.com/node trusty main' > /etc/apt/sources.list.d/nodesource.list
RUN echo 'deb-src https://deb.nodesource.com/node trusty main' >> /etc/apt/sources.list.d/nodesource.list
RUN apt-get update
RUN apt-get -qy install nodejs build-essential
