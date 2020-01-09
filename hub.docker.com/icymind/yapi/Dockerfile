FROM node:10.16.0-alpine
MAINTAINER SimonLu<luzuoqing@huya.com>

ENV YAPI_VER 1.7.0
ENV YAPI_URL https://github.com/YMFE/yapi/archive/v${YAPI_VER}.tar.gz

COPY config.json /

RUN set -ex \
	&& apk add --no-cache git python make \
	&& mkdir yapi && cd yapi \
	&& git clone --depth=1 https://github.com/YMFE/yapi vendors \
	&& mv /config.json . \
	&& cd vendors \
	&& npm install -production

WORKDIR /yapi/vendors

EXPOSE 8001
