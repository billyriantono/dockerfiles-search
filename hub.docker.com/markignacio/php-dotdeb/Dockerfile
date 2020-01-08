FROM php:7-apache
MAINTAINER Mark Ignacio <mark@ignacio.io>

# add dotdeb repository
ADD https://www.dotdeb.org/dotdeb.gpg /tmp/dotdeb.gpg
RUN apt-key add /tmp/dotdeb.gpg && \
    rm /tmp/dotdeb.gpg && \
    echo deb http://packages.dotdeb.org jessie all > /etc/apt/sources.list.d/dotdeb.list && \
    echo deb-src http://packages.dotdeb.org jessie all >> /etc/apt/sources.list.d/dotdeb.list && \
# do a lil' update
    apt-get update && \
    apt-get upgrade -y && \
    apt-get purge -y --auto-remove
