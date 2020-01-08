# docker friendly ubuntu 14.04 base image - https://github.com/phusion/baseimage-docker
FROM phusion/baseimage:0.9.11

MAINTAINER Thorben Stangenberg <thorben@stangenberg.net>

# Set correct environment variables.
ENV HOME /root

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Ensure we create the cluster with UTF-8 locale
RUN locale-gen en_US.UTF-8 && \
        echo 'LANG="en_US.UTF-8"' > /etc/default/locale

# Disable SSH 
RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh

# Add the PostgreSQL PGP key to verify their Debian packages.
# It should be the same key as https://www.postgresql.org/media/keys/ACCC4CF8.asc
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8 && \
  echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main 9.3" > /etc/apt/sources.list.d/pgdg.list && \
  apt-get update

# Install the latest postgresql version 9.3
RUN DEBIAN_FRONTEND=noninteractive \
    apt-get install -y --force-yes \
        postgresql-9.3 postgresql-contrib-9.3

# Install inotify-tools
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y inotify-tools

# Copy configuration files
ADD postgresql.conf /etc/postgresql/9.3/main/postgresql.conf
ADD pg_hba.conf /etc/postgresql/9.3/main/pg_hba.conf

# Add scripts
ADD scripts /scripts
RUN chmod +x /scripts/start.sh

# Add daemon to be run by runit.
RUN mkdir /etc/service/postgresql
RUN ln -s /scripts/start.sh /etc/service/postgresql/run

# Expose PostgreSQL default port
EXPOSE 5432

# Clean up when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/lib/postgresql /var/log/postgresql