# vim:set ft=dockerfile:

# Base on VRT Base image
FROM vrtsystems/baseimage:0.2.0
MAINTAINER VRT Engineering <engineering@vrt.com.au>

# add our user and group first to make sure their IDs get assigned
# consistently, regardless of whatever dependencies get added later
RUN groupadd -r nginx && useradd -r -g nginx nginx

ENV NGINX_VERSION 1.11.5-1~jessie

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
	&& echo "deb http://nginx.org/packages/mainline/debian/ jessie nginx" >> /etc/apt/sources.list \
	&& apt-get update \
	&& echo "=== Installing Nginx ===================" \
	&& apt-get install -y ca-certificates nginx=${NGINX_VERSION} \
	&& ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log \
	&& mkdir -p /usr/local/etc/docker-nginx/prestart-init.d \
	&& echo "=== Cleaning up ========================" \
	&& /usr/local/sbin/docker-cleanup.sh

ADD docker-entrypoint.sh /usr/local/sbin/
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/cache/nginx"]

EXPOSE 80 443

# CMD ["nginx", "-g", "daemon off;"]
ENTRYPOINT ["/usr/local/sbin/docker-entrypoint.sh"]

CMD ["supervisor"]
