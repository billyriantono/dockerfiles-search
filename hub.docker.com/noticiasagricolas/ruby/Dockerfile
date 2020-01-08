FROM ruby:2.2-jessie

ARG PHANTOM_JS_VERSION
ENV PHANTOM_JS_VERSION ${PHANTOM_JS_VERSION:-2.1.1-linux-x86_64}

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    aria2 \
    bzip2 \
    ca-certificates \
    cron \
    curl \
    libav-tools \
    libfontconfig \
    mysql-client \
    python-mysql.connector \
    s3cmd \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Install PhantonJS
RUN mkdir /tmp/phantomjs \
  && curl -L https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-${PHANTOM_JS_VERSION}.tar.bz2 \
    | tar -xj --strip-components=1 -C /tmp/phantomjs \
  && mv /tmp/phantomjs/bin/phantomjs /usr/local/bin \
  && rm -rf /tmp/*

# Clean unnecessary cron jobs
RUN rm -f /etc/cron.daily/apt \
    rm -f /etc/cron.daily/dpkg \
    rm -f /etc/cron.daily/password
