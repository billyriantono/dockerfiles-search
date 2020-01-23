FROM node:8.16.0-alpine
RUN apk add --no-cache \
	g++ \
	gcc \
	libgcc \
	libstdc++ \
	libuv \
	make \
	python \
 && apk add \
		build-base \
		fftw-dev \
		libc6-compat \
		vips-dev \
        --update-cache \
        --repository https://alpine.global.ssl.fastly.net/alpine/edge/community \
        --repository https://alpine.global.ssl.fastly.net/alpine/edge/main \
 && rm -fR /var/cache/apk/*

RUN apk --update --no-cache add \
	ca-certificates \
	curl \
	git \
	libcurl \
	openssh \
	openssl \
	&& rm -rf /var/cache/apk/*

EXPOSE 8000
RUN npm install --no-optional --no-shrinkwrap --no-package-lock --global --save \
	gatsby \
	gatsby-cli \
	gatsby-dev-cli \
	graphql \
	webpack \
	yarn


# create app directories
RUN mkdir -p /var/www/app
WORKDIR /var/www/app
EXPOSE 8000