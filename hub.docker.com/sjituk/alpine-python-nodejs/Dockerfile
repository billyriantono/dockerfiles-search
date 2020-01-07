# Grab base image
FROM python:alpine3.7

# Upgrade packages and install Node JS
RUN apk update && apk add --update "nodejs<9"

# Check nodejs and npm version
RUN node -v && npm -v

# Check Python version
RUN python3 --version

# App folder and set it work directory
ADD . /opt/app
WORKDIR /opt/app

# Add non root user
RUN adduser -D appuser
RUN chown -R appuser:appuser /opt/app
