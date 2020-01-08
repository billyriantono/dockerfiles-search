FROM php:7.2-fpm-alpine

LABEL maintainer="jjwood2004@gmail.com"

# persistent / runtime deps
RUN apk add --update \
		rsync \
		composer \
		nodejs==8.14.0-r0 \
		npm==8.14.0-r0 \
		openssh-client \
		bash