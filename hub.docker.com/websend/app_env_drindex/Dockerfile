# NAME: Application Dr Index Environment
#
# DESCRIPTION: Base for the Dr Index images.
#
# NEEDED ENVS:
#
# USAGE EXAMPLE: docker run websend/app_env_drindex

FROM websend/ruby:2.2.0
MAINTAINER Joost van Rijn <j.vanrijn@websend.nl>

ENV PHANTOMJS_VERSION 1.9.7

RUN \
  echo 'deb ftp://ftp.us.debian.org/debian/ wheezy non-free' >> /etc/apt/sources.list.d/wheezy.non-free.list && \
  echo 'deb http://security.debian.org/ wheezy/updates non-free' >> /etc/apt/sources.list.d/wheezy.non-free.list && \
  apt-get update && \
  apt-get install -yq curl && \
  curl -sL https://deb.nodesource.com/setup | bash - && \
  apt-get install -yq nodejs && \
  apt-get install -yq libmysqlclient-dev && \
  apt-get install -yq libcurl4-gnutls-dev && \
  apt-get install -yq imagemagick && \
  apt-get install -yq ghostscript && \
  apt-get install -yq vim && \
  apt-get install -yq git && \
  apt-get install -yq wget && \
  apt-get install -yq libfreetype6 && \
  apt-get install -yq libfontconfig && \
  apt-get install -yq bzip2 && \
  apt-get install -yq libsqlite3-dev && \
  apt-get install -yq unrar && \
  apt-get install -yq libpng12-dev && \
  apt-get install -yq libmagickcore-dev && \
  apt-get install -yq libmagickwand-dev && \
  apt-get install -yq inotify-tools && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
  groupadd -g 1001 apphoster && \
  useradd -u 998 -g 1001 -m apphoster

RUN \
  mkdir -p /srv/var && \
  wget -q --no-check-certificate -O /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  tar -xjf /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 -C /tmp && \
  rm -f /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  mv /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64/ /srv/var/phantomjs && \
  ln -s /srv/var/phantomjs/bin/phantomjs /usr/bin/phantomjs && \
  git clone https://github.com/n1k0/casperjs.git /srv/var/casperjs && \
  ln -s /srv/var/casperjs/bin/casperjs /usr/bin/casperjs && \
  apt-get autoremove -y && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN \
 cd /tmp && \
 wget ftp://ftp.foolabs.com/pub/xpdf/xpdf-3.04.tar.gz && \
 tar xvfz xpdf-3.04.tar.gz && \
 cd xpdf-3.04/ && \
 ./configure && \
 make && \
 make install

COPY policy.xml /etc/ImageMagick/policy.xml
