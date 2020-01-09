FROM        ubuntu:16.04
MAINTAINER  Hector Ros
 
ENV DEBIAN_FRONTEND noninteractive
ENV VCL_FILE default
ENV STORAGE "malloc,100M"
ENV VARNISH_PORT 80

# Update the package repository
RUN apt-get -qq update

# Install base system
RUN apt-get -qqq install -y curl gnupg apt-transport-https
RUN curl -L https://packagecloud.io/varnishcache/varnish5/gpgkey | apt-key add -
RUN apt-get -qq update
ADD varnishcache_varnish5.list /etc/apt/sources.list.d/varnishcache_varnish5.list
RUN apt-get -qqq install varnish

ADD start /start
RUN chmod 0755 /start

CMD ["/start"]
