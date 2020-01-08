FROM ruby:2.4

# Env
ENV PHANTOMJS_VERSION 2.1.1

# Install phantomjs
RUN \
  apt-get update && \
  apt-get install -y --no-install-recommends node-uglify libfontconfig && \
  wget -q --no-check-certificate -O /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 \
      https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  tar -xjf /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 -C /tmp && \
  rm -f /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  mv /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64/bin/phantomjs /usr/bin/phantomjs && \
  rm -rf /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64 && \
  apt-get autoremove -y && \
  apt-get clean all && \
  rm -rf /var/lib/apt/lists/* &&\
  echo -n PhantomJS Version: && \
  phantomjs -v && \
  echo -n Current User: && \
  whoami