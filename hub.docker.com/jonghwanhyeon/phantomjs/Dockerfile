FROM debian:buster-slim

LABEL maintainer="hyeon0145@gmail.com"

ENV PHANTOMJS_VERSION 2.1.1

RUN apt-get update && apt-get install -y \
    libssl-dev \
    libfontconfig1 \
    curl \
    bzip2 \
&& rm -rf /var/lib/apt/lists/*

RUN curl --location https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-${PHANTOMJS_VERSION}-linux-x86_64.tar.bz2 | tar xj -C /usr/local/share/

RUN apt-get purge --auto-remove -y \
    curl \
    bzip2

ENV OPENSSL_CONF /etc/ssl/
RUN ln -s /usr/local/share/phantomjs-${PHANTOMJS_VERSION}-linux-x86_64/bin/phantomjs /usr/local/bin

ENTRYPOINT ["phantomjs"]
