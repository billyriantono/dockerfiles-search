FROM debian:jessie
MAINTAINER BIG FISH <huszy@bigfish.hu>

ENV DEBIAN_FRONTEND=noninteractive
#
# Install Node.js 10.x
#
RUN apt-get update && apt-get install -y apt-transport-https wget

ENV NODEJS_VERSION 10.11.0-1nodesource1

RUN wget -qO- https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - \
	&& echo 'deb https://deb.nodesource.com/node_10.x jessie main' >> /etc/apt/sources.list \
	&& echo 'deb-src https://deb.nodesource.com/node_10.x jessie main' >> /etc/apt/sources.list

RUN apt-get update && apt-get install -y nodejs

RUN npm install -g yarn
