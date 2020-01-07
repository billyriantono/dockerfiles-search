FROM node:latest

MAINTAINER Kentaro Terada kterada.0509sg@gmail.com

RUN set -x \
    # Install npm packages
    && npm install -g s3-proxy s3rver\

    # Create Data directory
    && mkdir -p /data

CMD ["s3rver", "-d", "/data", "-p", "8080", "-h", "0.0.0.0"]

EXPOSE 8080
