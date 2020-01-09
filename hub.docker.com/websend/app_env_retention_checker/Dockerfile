# NAME: Application Retention Checker Environment
#
# DESCRIPTION: Base for other the Retention Checker images.
#
# NEEDED ENVS:
#
# USAGE EXAMPLE: docker run websend/app_env_retention_checker

FROM websend/ruby:2.1.2
MAINTAINER Gerard Meijer <g.meijer@websend.nl>

RUN \
  apt-get update && \
  apt-get install -yq curl && \
  curl -sL https://deb.nodesource.com/setup | bash - && \
  apt-get install -yq nodejs && \
  apt-get install -yq libcurl4-gnutls-dev && \
  apt-get install -yq libmysqlclient-dev && \
  apt-get install -yq libfreetype6 && \
  apt-get install -yq libfontconfig && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
  useradd -u 6666 -m apphoster

  ENV PHANTOMJS_VERSION 1.9.7
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
