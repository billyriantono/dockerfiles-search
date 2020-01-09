FROM ubuntu:18.04
LABEL maintainer "Alex Haydock <alex@alexhaydock.co.uk>"

# Setup Environment for Ubuntu
ENV DEBIAN_FRONTEND noninteractive

RUN set -xe \
    \
# Update package list
    && apt-get update \
    \
# Add a package
    && apt-get -y install ncmpcpp \
    \
# Clear package cache to save space
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/

ENTRYPOINT ["/usr/bin/ncmpcpp","--config","/config/ncmpcpp.conf"]