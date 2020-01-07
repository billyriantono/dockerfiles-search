FROM ubuntu:16.04

maintainer James Kyburz "james.kyburz@gmail.com"

RUN \
  apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62\
  && echo "deb http://nginx.org/packages/mainline/ubuntu/ xenial nginx\ndeb-src http://nginx.org/packages/mainline/ubuntu/ xenial nginx" >> /etc/apt/sources.list\
  && apt-get update \
  && apt-get install --no-install-recommends --no-install-suggests -y \
  openssl \
  nginx \
  ca-certificates \
  nginx-module-xslt \
  nginx-module-geoip \
  nginx-module-image-filter \
  nginx-module-perl \
  nginx-module-njs \
  gettext-base \
	&& rm -rf /var/lib/apt/lists/*

RUN mkdir -p /etc/nginx/ssl/

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
