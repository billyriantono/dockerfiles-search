FROM ubuntu:xenial
MAINTAINER Iakov Kirilenko <Iakov.Kirilenko@trikset.com>
ENV DEBIAN_FRONTEND noninteractive
ARG CHECKER_TAG=latest
#Run everything at once to create a single layer
RUN set -eu \
    && apt-get update \
    && apt-get install -y --no-install-recommends locales apt-utils \
    && apt-get -y dist-upgrade \
    && apt-get install -y --no-install-recommends \
               libbsd0 libdbus-1-3 libexpat1 libwrap0 \
	       libpng12-0 libglib2.0-0 libjson-c2 \
	       curl ca-cacert xz-utils \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
            /var/cache/debconf/* \
            /usr/share/doc \
            /usr/share/man \
            /usr/share/locale/?? \
            /usr/share/locale/??_?? \
    && locale-gen --purge ru_RU.UTF-8
RUN du -csh /* 2>/dev/null | sort -h || :
