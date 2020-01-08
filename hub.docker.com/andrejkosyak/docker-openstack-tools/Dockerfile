FROM alpine:latest

MAINTAINER Andre Kosak "andrekosak@icloud.com"

LABEL Description="Provides openstack client tools" Version="1.0"

# Alpine-based installation
# #########################
RUN apk add --update \
  # bash \
  python-dev \
  py-pip \
  py-setuptools \
  ca-certificates \
  gcc \
  musl-dev \
  libffi-dev libressl-dev \
  linux-headers \
  && pip install --upgrade --no-cache-dir pip setuptools python-openstackclient \
  python-swiftclient==3.3.0 python-keystoneclient python-heatclient \
  && apk del gcc musl-dev linux-headers \
  && rm -rf /var/cache/apk/*

# Add a volume so that a host filesystem can be mounted 
VOLUME ["/data"]

# Default is to start a shell.  A more common behavior would be to override
# the command when starting.
CMD ["/bin/sh"]