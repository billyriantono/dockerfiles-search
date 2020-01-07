# This is based on the official Alpine Dockerfile for nginx.
#
# It takes the default configs from that container and enables gzip,
# and autoindexing, and it listens only on port 8080 so that nginx
# can be launched without root privileges.

FROM nginx:stable-alpine
LABEL maintainer "Alex Haydock <alex@alexhaydock.co.uk>"

ADD nginx.conf /etc/nginx/nginx.conf
ADD default.conf /etc/nginx/conf.d/default.conf

RUN set -xe \
    \
# Add shadow to modify UID of nginx user and group (--no-cache saves space by creating no local package cache)
    && apk --no-cache add shadow \
    \
# Modify the UID and GID of the automatically-enabled 'nginx' user and group to 1000
    && usermod -u 1000 nginx \
    && groupmod -g 1000 nginx \
    \
# Remove shadow package to decrease attack surface
    && apk del shadow

# Run
CMD ["nginx", "-g", "daemon off;"]
