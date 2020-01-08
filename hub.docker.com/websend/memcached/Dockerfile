# Build: docker build -t websend/memcached:latest .

FROM websend/debian:7.7
MAINTAINER Ilja Krijger <i.krijger@websend.nl>

RUN \
  apt-get -q update && \
  apt-get -yq install memcached  && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER daemon

EXPOSE 11211

ENTRYPOINT ["memcached", "-vvv"]