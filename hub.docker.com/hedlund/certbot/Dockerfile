# Minimal Certbot Docker image
# Based off Debian Jessie to keep it similar to the Nginx image...

FROM debian:jessie
MAINTAINER Henrik Hedlund <henrik@hedlund.im>

ENV DEBIAN_FRONTEND=noninteractive

# Add Debian Backports & install Certbot
RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get install --no-install-recommends --no-install-suggests -y certbot -t jessie-backports

# Export certificate volume
VOLUME /etc/letsencrypt/

ENTRYPOINT [ "certbot" ]
