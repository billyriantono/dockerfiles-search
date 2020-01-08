# Openstack CLI

FROM alpine:latest
LABEL maintainer "Jonathan Roemer <dev@roemersoftworks.com>"

RUN apk update && apk upgrade && apk --no-cache add \
    build-base python3 python3-dev \
    libffi-dev openssl-dev bash

RUN pip3 install openstackclient

# Set up a non-root user for the program
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
WORKDIR /home/appuser
USER appuser

ENTRYPOINT [ "openstack" ]
