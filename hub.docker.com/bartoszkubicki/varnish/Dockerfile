FROM debian:stretch
MAINTAINER Bartosz Kubicki <b.w.kubicki@gmail.com>

#Installation
RUN apt-get update \
&& apt-get -y install vim curl gnupg gettext-base apt-transport-https debian-archive-keyring \
&& curl -L https://packagecloud.io/varnishcache/varnish61/gpgkey | apt-key add - \
&& touch /etc/apt/sources.list.d/varnishcache_varnish61.list \
&& echo 'deb https://packagecloud.io/varnishcache/varnish61/debian/ stretch main' > /etc/apt/sources.list.d/varnishcache_varnish61.list \
&& echo 'deb-src https://packagecloud.io/varnishcache/varnish61/debian/ stretch main' >> /etc/apt/sources.list.d/varnishcache_varnish61.list \
&& apt-get update \
&& apt-get install -y varnish=6.1.1-1~stretch \
&& apt-get clean

#User configuration
RUN usermod -u 1000 www-data
RUN groupadd varnishlog && usermod -G varnishlog varnish

#Envirnoment variables
ENV VARNISH_LISTEN_ADDRESS ''
ENV VARNISH_LISTEN_PORT 80
ENV VARNISH_VCL_CONF /etc/varnish/default.vcl
ENV VARNISH_ADMIN_LISTEN_ADDRESS 127.0.0.1
ENV VARNISH_ADMIN_LISTEN_PORT 6082
ENV VARNISH_TTL 120
ENV VARNISH_CACHE_SIZE 256M
ENV VARNISH_DAEMON_CONF /etc/default/varnish

#Add default configuration and default deamon options
COPY default.vcl $VARNISH_VCL_CONF
COPY varnish /tmp/varnish.dist

#Handle default daemon conf file
RUN chmod u+x /tmp/varnish.dist
RUN envsubst < /tmp/varnish.dist > $VARNISH_DAEMON_CONF
RUN rm /tmp/varnish.dist

#Add start script with proper permissions
ADD ./start.sh /start.sh
RUN chmod +x /start.sh

#Exposing port
EXPOSE $VARNISH_LISTEN_PORT $VARNISH_ADMIN_LISTEN_PORT

#Start varnish deamon
CMD /start.sh
