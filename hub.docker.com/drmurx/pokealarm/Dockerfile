# Basic docker image for PokeAlarm
# It runs with the webhook -wh http://127.0.0.1:4000
# Usage:
#   docker build -t pokealarm
#   docker run -d --net container:RocketMap --name PokeAlarm -P pokealarm
# Change "RocketMap" to the name of your RocketMap docker
# For newer versions of docker maybe you have to change --net to --network

FROM python:2.7-alpine

# Default port the webserver runs on
EXPOSE 4000

# Working directory for the application
WORKDIR /usr/src/app

# Entrypoint script
ENTRYPOINT ["/usr/src/app/tools/docker-entrypoint.sh"]

# Install required system packages
RUN apk add --no-cache ca-certificates bash openssh inotify-tools

COPY requirements.txt /usr/src/app/

RUN apk add --no-cache git build-base \
 && pip install --no-cache-dir -r requirements.txt \
 && apk del git build-base

# Copy everything to the working directory (Python files, templates, config) in one go.
COPY . /usr/src/app/
