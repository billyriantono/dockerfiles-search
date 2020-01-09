# Use builds from launchpad
FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive

RUN \
apt-get update && \
apt-get -y dist-upgrade && \
apt-get install -y software-properties-common && \
add-apt-repository -y ppa:opencpu/opencpu-2.1 && \
apt-get update && \
apt-get install -y opencpu-server

# Prints apache logs to stdout
RUN \
ln -sf /proc/self/fd/1 /var/log/apache2/access.log && \
ln -sf /proc/self/fd/1 /var/log/apache2/error.log && \
ln -sf /proc/self/fd/1 /var/log/opencpu/apache_access.log && \
ln -sf /proc/self/fd/1 /var/log/opencpu/apache_error.log

# Set opencpu password so that we can login
RUN \
echo "opencpu:opencpu" | chpasswd

# Apache ports
EXPOSE 80
EXPOSE 443
EXPOSE 8004


# Install development tools
RUN \
apt-get install -y rstudio-server r-base-dev sudo curl git libcurl4-openssl-dev libssl-dev libxml2-dev libssh2-1-dev

# Workaround for rstudio apparmor bug
RUN echo "server-app-armor-enabled=0" >> /etc/rstudio/rserver.conf

CMD service cron start && /usr/lib/rstudio-server/bin/rserver && apachectl -DFOREGROUND

