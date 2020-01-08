FROM ubuntu:latest
MAINTAINER Mark Williams <m2kw6s@gmail.com>

# Update the package repository and install packages
RUN apt-get update \
    && apt-get install -q -y supervisor nagios-nrpe-server nagios-plugins arping nmap \
       && apt-get clean \
       && rm -rf /var/lib/apt /tmp/* /var/tmp/*

# Configure timezone
RUN echo "America/Los_Angeles" > /etc/timezone; dpkg-reconfigure -f noninteractive tzdata

EXPOSE 5666

# Add custom files
COPY files/root /
 
# Start command
CMD ["/start"]

