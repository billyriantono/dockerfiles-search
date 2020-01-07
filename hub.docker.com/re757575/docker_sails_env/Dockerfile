# https://hub.docker.com/r/library/node/
FROM node:4

# INSTALL git vim curl
RUN apt-get update && \
	apt-get install -y git vim curl && \
	git config --global url."https://".insteadOf git:// && \

	# INSTALL GLOBAL PACKAGE
	npm install -g -q bower gulp &&\

	# CLEAR CACHE
	apt-get autoclean && apt-get clean && \
	rm -rf /var/lib/apt/lists/*
