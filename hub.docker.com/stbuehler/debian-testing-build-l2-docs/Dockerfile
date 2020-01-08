FROM debian:testing

MAINTAINER Stefan Bühler <stbuehler@lighttpd.net>

# don't install recommended dependencies
COPY apt.conf.no-recommends /etc/apt/apt.conf.d/no-recommends

# adduser + build user with uid/gid 20001
RUN apt-get update \
	&& apt-get install -y \
		adduser \
	&& addgroup --gid 20001 build \
	&& adduser --uid 20001 --gid 20001 --disabled-password --gecos "" build

# ruby + some gems, libxml2-utils and rsync
RUN apt-get install -y \
		ruby ruby-nokogiri ruby-bluecloth ruby-redcloth \
		libxml2-utils \
		rsync

USER build
