# Dockerfile - Ubuntu Bionic
# https://github.com/openresty/docker-openresty

ARG RESTY_IMAGE_BASE="openresty/openresty"
ARG RESTY_IMAGE_TAG="bionic"

FROM ${RESTY_IMAGE_BASE}:${RESTY_IMAGE_TAG}

LABEL maintainer="Tomas Zvala <tomas@zvala.cz>"


RUN export DEBIAN_FRONTEND=noninteractive \
	&& cd /usr/local/src \
	&& apt-get update \
	&& apt-get -y --no-install-recommends install git python 
RUN cd /usr/local/src \
	&& git clone https://github.com/p0pr0ck5/lua-resty-waf.git \
	&& cd lua-resty-waf \
	&& git checkout -b development \
	&& git submodule update --init
COPY resty.patch /usr/local/src
RUN cd /usr/local/src/lua-resty-waf \
	&& patch -p1 < /usr/local/src/resty.patch \
	&& make && make install
RUN rm /usr/local/openresty/nginx/logs/*

VOLUME /usr/local/openresty/nginx/conf
VOLUME /usr/local/openresty/nginx/logs

COPY start.sh /usr/local/openresty/start.sh

CMD ["/usr/local/openresty/start.sh"]
