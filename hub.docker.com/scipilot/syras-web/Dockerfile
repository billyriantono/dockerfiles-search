#
# Docker build for the SYRAS Systematic Review Assistant ExpressJS application.
#
# It should be used in a Docker composition:
# 	https://hub.docker.com/r/scipilot/sysrev-assist-web
# 	See docker-compose.yaml for details.
#
# Environment requirements:
# 	$SYSREV_DOMAIN,
# 	$NODE_ENV
#	"/etc/letsencrypt" volume
#
# todo: currently assumes gulp src is pre-built and baked into express/public/css, js
#
FROM node:8-alpine

ENV HOME=/app

# Install codebase
RUN mkdir /app
COPY . /app/sysrev-assist

# Build app and clean up in one command to reduce image size
RUN apk --update add --no-cache --virtual .build-deps git && \
    cd /app/sysrev-assist/express && npm install && \
    apk del .build-deps

# This is the "bare" alternative to the systemd service (in sysrev-assist/etc).
# This command asumes you will use Docker's auto-restart.
WORKDIR /app/sysrev-assist/express
CMD bin/www
