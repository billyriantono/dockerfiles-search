FROM node:8-alpine
MAINTAINER developmentteamserenity@fasthosts.com

RUN apk add --no-cache git \
	&& mkdir -p \
		/app \
		/tmp/npm \
	&& chown -R 1000:1000 \
		/app \
		/tmp

WORKDIR /app/

USER 1000
ENV HOME /tmp
ENV PATH="/tmp/npm/bin:${PATH}"
RUN npm config set prefix /tmp/npm