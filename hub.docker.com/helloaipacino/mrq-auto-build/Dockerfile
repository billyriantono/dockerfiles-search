FROM ubuntu:12.04

#
# httpredir.debian.org is often unreliable
# https://github.com/docker-library/buildpack-deps/issues/40
#

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
RUN echo "deb http://repo.mongodb.org/apt/ubuntu precise/mongodb-org/3.2 multiverse" > /etc/apt/sources.list.d/mongodb-org-3.2.list
RUN apt-get update && \
	apt-get install -y --no-install-recommends \
				mongodb-org-server \
	&& \
	apt-get clean -y && \
	rm -rf /var/lib/apt/lists/*

RUN mkdir -p /data/db

VOLUME ["/data"]
WORKDIR /app

# Redis and MongoDB services
EXPOSE 6379 27017

# Dashboard, monitoring and docs
EXPOSE 5555 20020 8000