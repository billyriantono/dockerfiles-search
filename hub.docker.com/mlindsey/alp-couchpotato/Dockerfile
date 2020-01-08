## Dockerfile for Couchpotato, using Alpine base.
FROM alpine:3.2
MAINTAINER mlindsey@fastmail.com.au

# Add additional repo's to APK
# RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
# RUN echo "@edge http://nl.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories
# RUN echo "@communities http://nl.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories

## Install Dependancies and Application
RUN apk update
RUN apk add git python && \
    rm -rf /var/cache/apk/*

# Add additional files.
ADD assets/start.sh /start.sh
RUN chmod a+x /start.sh

# Install Couchpotato
RUN mkdir /opt && git clone https://github.com/RuudBurger/CouchPotatoServer.git /opt/CouchPotato

# Expose Ports
EXPOSE 5050

# Add Volumes
VOLUME /config
VOLUME /data

## Command to run
CMD ["/start.sh"]
