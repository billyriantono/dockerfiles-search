FROM node:8

MAINTAINER BAREXTE <barexte@gmail.com>

# Copy start script
COPY ./start.sh /usr/bin/
RUN chmod +x /usr/bin/start.sh

# create dirs
RUN mkdir -p /app && chown 1001:1001 /app
RUN mkdir -p /config && chown 1001:1001 /config
RUN mkdir -p /data && chown 1001:1001 /data

# switch user
USER 1001

ENV HOME=/app
WORKDIR /app

# 
EXPOSE 10000

VOLUME /config
VOLUME /data

# Entrypoint
ENTRYPOINT ["start.sh"]
