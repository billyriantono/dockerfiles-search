FROM ubuntu:14.04

MAINTAINER Brad Bowman <brad@newmediadenver.com>

ENV NGINX_VERSION=1.9.7
ENV NGINX_SHA256=794bd217affdfce1c6263d9199c3961f387a2df9d57dcb42876faaf41c1748d5
ENV LDAP_SRC_DIR=/tmp/src/nginx-ldap
ENV NGINX_LDAP_VERSION=be8ff8ee

RUN groupadd nginx && useradd --create-home --home-dir /home/nginx -g nginx nginx

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y \
  && apt-get install -y -q build-essential git supervisor curl libpcre3-dev libldap2-dev libssl-dev

ADD http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz /tmp/nginx.tar.gz

RUN echo "${NGINX_SHA256} */tmp/nginx.tar.gz" | sha256sum -c - \
  && cd /tmp \
  && tar -xvf nginx.tar.gz \
  && mkdir -p ${LDAP_SRC_DIR} \
  && git clone --depth 1 https://github.com/kvspb/nginx-auth-ldap.git ${LDAP_SRC_DIR} \
  && cd ${LDAP_SRC_DIR} \
  && git reset --hard ${NGINX_LDAP_VERSION} \
  && cd /tmp/nginx-${NGINX_VERSION} \
  && ./configure --user=nginx --group=nginx --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-http_gzip_static_module --with-http_stub_status_module --with-http_ssl_module --with-pcre --with-file-aio --with-http_realip_module --add-module=${LDAP_SRC_DIR} --with-ipv6 --with-debug \
  && make \
  && make install \
  && rm -rf ../nginx.tar.gz \
  && rm -rf ${LDAP_SRC_DIR}


COPY files /

RUN chmod ugo+x start-nginx.sh

EXPOSE 80 443

CMD ["/usr/bin/supervisord"]
