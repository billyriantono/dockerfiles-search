# Parent image
FROM barexte/vuejs:latest

MAINTAINER BAREXTE <barexte@gmail.com>

# global environment settings
ENV SERVER_PORT="8080"

# Copy start script
COPY ./start.sh /usr/bin/
RUN chmod +x /usr/bin/start.sh

# create dirs
RUN mkdir -p /app && chown 1001:1001 /app

# setup user
USER 1001

ENV HOME=/app
WORKDIR /app

# 
EXPOSE 8080
VOLUME /app

# Entrypoint
ENTRYPOINT ["start.sh"]
