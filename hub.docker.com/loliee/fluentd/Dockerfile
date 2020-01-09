# Fluentd

FROM ruby:2.2.0
MAINTAINER Maxime Loliée <maxime@siliadev.com>
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y \
    gcc\
    libcurl4-gnutls-dev \
    make

RUN gem install fluentd -v "~>0.12.12" && mkdir -p /etc/fluent
RUN /usr/local/bin/gem install fluent-plugin-elasticsearch

RUN apt-get remove -y --auto-remove gcc make ruby-dev && \
    apt-get clean  && \
    rm -rf /var/lib/apt/lists/*

ADD files/fluent.conf /etc/fluent/fluent.conf

VOLUME ["/etc/fluent/"]

ENTRYPOINT ["/usr/local/bundle/bin/fluentd", "-c", "/etc/fluent/fluent.conf"]
