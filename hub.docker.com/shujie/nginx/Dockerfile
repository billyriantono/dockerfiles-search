FROM alpine
MAINTAINER shujie
RUN apk update
RUN apk upgrade
RUN apk add nginx
RUN apk add owncloud-pgsql php-fpm
CMD ["app:start"]
