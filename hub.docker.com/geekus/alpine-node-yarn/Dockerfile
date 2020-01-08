FROM alpine:3.5

MAINTAINER ContainerShip Developers <developers@containership.io>

ARG YARN_VERSION=0.19.1
ARG NODE_VERSION=6.9.2-r1

ENV PATH /root/.yarn/bin:$PATH

RUN apk add --update --no-cache nodejs=${NODE_VERSION} \
	&& touch ~/.bashrc \
	&& apk add --no-cache --virtual .build-deps-yarn tar curl bash gnupg \
	&& rm -rf /var/cache/apk/* \
	&& curl -o- -L https://yarnpkg.com/install.sh | bash -s -- --version ${YARN_VERSION} \
	&& apk del .build-deps-yarn \
	&& npm uninstall -g npm \
	&& rm -rf ~/.gnupg ~/.npm

