FROM debian:9

RUN apt-get update -qq \
	&& apt-get install -y -qq lftp build-essential curl \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
