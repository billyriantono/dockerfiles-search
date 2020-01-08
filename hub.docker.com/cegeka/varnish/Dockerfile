FROM debian:jessie

# Add repositories
RUN apt-get update -qq && \
    apt-get -yqq install curl

RUN curl -s https://packagecloud.io/install/repositories/varnishcache/varnish41/script.deb.sh | bash

# Update the package repository and install applications
RUN apt-get update -qq && \
  apt-get upgrade -yqq && \
  apt-get -yqq install varnish && \
  apt-get -yqq clean

# Make our custom VCLs available on the container
RUN mkdir /docker-vcl-initdb.d

ENV VARNISH_BACKEND_PORT 8080
ENV VARNISH_BACKEND_HOST 127.0.0.1
ENV VARNISH_PORT 80
ENV VARNISH_VCL default.vcl

COPY docker-entrypoint.sh /

# Expose port 80
EXPOSE 80

CMD ["/docker-entrypoint.sh"]
