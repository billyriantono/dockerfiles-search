FROM phusion/baseimage:latest
MAINTAINER Jonathon Leight <jonathon.leight@jleight.com>

ENV NGINX_VERSION  1.7.10-1~wheezy
ENV NGINX_REPO     http://nginx.org/packages/mainline/debian
ENV NGINX_APT_LIST /etc/apt/sources.list.d/nginx.list

RUN set -x \
  && apt-key adv \
    --keyserver keyserver.ubuntu.com \
    --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
  && echo "deb ${NGINX_REPO} wheezy nginx" > "${NGINX_APT_LIST}" \
  && apt-get update \
  && apt-get install -y ca-certificates nginx=${NGINX_VERSION} \
  && ln -sf /dev/stdout /var/log/nginx/access.log \
  && ln -sf /dev/stderr /var/log/nginx/error.log \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
    /tmp/* \
    /var/tmp/*

ADD nginx-service.sh /etc/service/nginx/run

EXPOSE 80
EXPOSE 443
VOLUME ["/usr/share/nginx/html"]