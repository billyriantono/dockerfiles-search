# set base image
FROM debian:latest 

# author
MAINTAINER Nathan Thisler

# extra metadata
LABEL version="1.0"

LABEL description="Apt-Cacher-NG Docker v1.0"

VOLUME ["/var/cache/apt-cacher-ng"]
RUN apt-get update && apt-get install -y apt-cacher-ng
RUN sed 's/\# PassThroughPattern\: \.\*/PassThroughPattern\: \.\*/' /etc/apt-cacher-ng/acng.conf > /tmp/acng.conf && rm /etc/apt-cacher-ng/acng.conf && mv /tmp/acng.conf /etc/apt-cacher-ng/

EXPOSE 3142
CMD chmod 777 /var/cache/apt-cacher-ng && /etc/init.d/apt-cacher-ng start && tail -f /var/log/apt-cacher-ng/*
