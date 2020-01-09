# Install the latest haskell-platform package from Ubuntu trusty repository
FROM debian:latest
MAINTAINER contact@thachmai.info

RUN apt-get update \
	&& apt-get -y install haskell-platform \
        && apt-get clean \
        && rm -rf /var/cache/apt/archives/*

VOLUME /src
WORKDIR /src

