#
# Dockerfile for nginx
#

FROM nginx:alpine
MAINTAINER kev <dongpingmax@163.com>

VOLUME /usr/share/nginx/html /var/log/nginx

RUN set -xe \
    && chmod 766 /usr/share/nginx/html \
	&& chmod 766 /var/log/nginx