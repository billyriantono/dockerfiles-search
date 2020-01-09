# Copyright (c) 2015 Mattermost, Inc. All Rights Reserved.
# See License.txt for license information.
FROM ubuntu:14.04

RUN apt-get update \
	&& apt-get -y upgrade \
	&& export DEBIAN_FRONTEND=noninteractive \
	&& apt-get -y install wget netcat \
	&& rm -rf /var/lib/apt/lists/*

# Copy over files
RUN wget https://github.com/mattermost/platform/releases/download/v2.0.0/mattermost.tar.gz \
	&& tar -zxvf /mattermost.tar.gz --strip-components=1 && rm /mattermost.tar.gz

WORKDIR /mattermost

#start mattermost
RUN /mattermost/bin/platform -config=/mattermost/config.json

# Ports
EXPOSE 80
