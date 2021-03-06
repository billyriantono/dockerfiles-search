# CasperJS using PhantomJS

# VERSION 1.0.0

FROM daald/ubuntu32:trusty

ENV PHANTOMJS_VERSION_F 1.9.8
ENV CASPERJS_VERSION_F 1.1-beta3

RUN \
  apt-get update && \
  apt-get upgrade -y

# Configure locales
RUN locale-gen en_US.UTF-8

# Set default locale for the environment
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8


RUN \
  apt-get install -y libfreetype6-dev libfontconfig1-dev wget bzip2 unzip python && \

  mkdir -p /srv/var && \

  # download and install PhantomJS
  wget --no-check-certificate -O /tmp/phantomjs-$PHANTOMJS_VERSION_F-linux-i686.tar.bz2 https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-$PHANTOMJS_VERSION_F-linux-i686.tar.bz2 && \
  tar -xjf /tmp/phantomjs-$PHANTOMJS_VERSION_F-linux-i686.tar.bz2 -C /tmp && \
  rm -f /tmp/phantomjs-$PHANTOMJS_VERSION_F-linux-i686.tar.bz2 && \

  mv /tmp/phantomjs-$PHANTOMJS_VERSION_F*/ /srv/var/phantomjs && \
  ln -s /srv/var/phantomjs/bin/phantomjs /usr/bin/phantomjs && \

  # download and install CasperJS
  wget --no-check-certificate -O /tmp/casperjs-$CASPERJS_VERSION_F https://github.com/n1k0/casperjs/zipball/$CASPERJS_VERSION_F && \
  unzip /tmp/casperjs-$CASPERJS_VERSION_F -d /tmp && \
  rm -f /tmp/casperjs-$CASPERJS_VERSION_F && \

  mv /tmp/n1k0-casperjs-*/ /srv/var/casperjs && \
  ln -s /srv/var/casperjs/bin/casperjs /usr/bin/casperjs && \

  # clean up
  apt-get autoremove -y && \
  apt-get clean all && \
  rm -rf /var/lib/apt/lists/*

# Default command
ENTRYPOINT ["casperjs"]
CMD ["--help"]
