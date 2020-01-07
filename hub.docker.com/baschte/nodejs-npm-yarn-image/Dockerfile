FROM ubuntu:14.04
RUN mkdir -p /data/server \
	&& apt-get update && apt-get upgrade -y \
	&& apt-get install -y \
	curl

RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - \
	&& sudo apt-get install -y nodejs \
	&& sudo npm -g install npm@latest-2 \
	&& sudo npm -g install yarn \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
