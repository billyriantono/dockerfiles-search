FROM rdeville/baseimage
MAINTAINER Romain Deville <romain.deville1@gmail.com>

ENV \
# set list of package to install
  APTLIST="apache2" \
# set correct environment variables
  LANG="en_US.UTF-8"  \
  LANGUAGE="en_US:en"

# add some local files
COPY root/ /tmp/root/

RUN  \
# set the locale
  locale-gen $LANG && \
# install main packages
  apt-get update -q && \
  apt-get install $APTLIST -yqq && \
# enable apache mods in config
  a2enmod \
    actions \
    rewrite \
    alias \
    ssl \
    proxy \
    proxy_http \
    proxy_ajp \
    deflate \
    substitute \
    headers \
    proxy_balancer \
    proxy_connect \
    proxy_html \
    xml2enc \
    authnz_ldap && \
# avoid docker hub error because of copying to /
  cp -r /tmp/root/* / && \
# cleanup
  apt-get clean && \
  rm -rf \
    /var/lib/apt/lists/* \
    /tmp/* \
    /var/tmp/*

# ports and volumes
EXPOSE 80 443
VOLUME /config
