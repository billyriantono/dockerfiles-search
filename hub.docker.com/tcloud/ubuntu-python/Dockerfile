# Version 1.0
FROM tcloud/ubuntu-base:latest
MAINTAINER tcloud

# Install Python & PIP
RUN \
    apt-get update; \
    apt-get install -y -qq python-dev python-pip python-distro-info; \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["/sbin/my_init"]