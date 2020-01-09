# Squid Dockerfile.
FROM icsoft/baseimage

ARG LISTENPORT=3128

LABEL vendor="Icsoft Pty Ltd"

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Install the essentials for the build.
RUN apt-get update \
    && apt-get upgrade -y  -o Dpkg::Options::="--force-confold" \
    && apt-get install -y squid \
    && mkdir /etc/service/squid \    
    # Clean up
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

# Setup the service for baseimage-docker to run on start.
COPY squid.sh /etc/service/squid/run

# Enable access for configuration files and to view log files.
VOLUME /var/spool/squid
VOLUME /var/log/squid
VOLUME /etc/squid/conf.d

# Hint for port.
EXPOSE ${LISTENPORT}
