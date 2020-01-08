FROM nginx:1.10

MAINTAINER Ali Al Amine

ENV NGINX-NODE-VERSION 1.0

RUN apt-get update \
	&& apt-get install -y curl \
	&& curl -sL https://deb.nodesource.com/setup_4.x | bash - \
	&& apt-get install -y nodejs \
	&& npm install npm -g \
	&& apt-get remove -y --purge curl; apt-get -y autoremove \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
