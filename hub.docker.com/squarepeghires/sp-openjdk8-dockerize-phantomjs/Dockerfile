FROM squarepeghires/sp-openjdk8-dockerize:latest

# Install dependencies and tools
RUN \
  apt-get update && \
  apt-get install wget tar curl vim libfreetype6 fontconfig libfontconfig bzip2 -y && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/wget && \
  rm -rf /var/cache/tar && \
  rm -rf /var/cache/curl

ENV PHANTOMJS_VERSION=2.1.1

# Install PhantomJS
RUN \
  mkdir -p /srv/var && \
  wget -q --no-check-certificate -O /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  tar -xjf /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 -C /tmp && \
  rm -f /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  mv /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64/ /srv/var/phantomjs && \
  ln -s /srv/var/phantomjs/bin/phantomjs /usr/bin/phantomjs && \
  phantomjs --version
