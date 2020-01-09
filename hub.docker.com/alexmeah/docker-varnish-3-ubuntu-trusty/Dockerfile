FROM ubuntu:trusty

#Make Work Directories
RUN mkdir -p /build 
WORKDIR /build

# Install Varnish Key and Repo
RUN apt-get update -y \
  && apt-get install curl -y \
  && apt-get install apt-transport-https -y \
  && curl https://repo.varnish-cache.org/GPG-key.txt | apt-key add - \
  && echo "deb https://repo.varnish-cache.org/ubuntu/ trusty varnish-3.0" | tee -a /etc/apt/sources.list.d/varnish-cache.list \
  && echo "deb-src https://repo.varnish-cache.org/ubuntu/ trusty varnish-3.0" | tee -a /etc/apt/sources.list.d/varnish-cache.list

# Install Varnish
RUN apt-get update -y \
  && apt-get install dpkg-dev -y \
  && apt-get source varnish=3.0.7-1 -y \
  && apt-get build-dep varnish=3.0.7-1 -y

# Install libhiredis for Redis session lookup module
RUN apt-get install libhiredis-dev -y

# Build Source
RUN cd /build/varnish-3.0.7 \
 && dpkg-buildpackage -us -uc \
 && chmod -R 777 .
