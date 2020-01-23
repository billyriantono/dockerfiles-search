# Download base image ubuntu 16.04
FROM ubuntu:16.04

# Add the Ocata repo
RUN apt-get update && apt-get install -y software-properties-common \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
RUN add-apt-repository cloud-archive:ocata

# Update Ubuntu Software repository
RUN apt-get update && apt-get -y dist-upgrade

RUN apt-get -y install openstack-dashboard apache2 libapache2-mod-wsgi python-memcache
RUN apt-get -y purge openstack-dashboard-ubuntu-theme

EXPOSE 80

# Run apache in the foreground
RUN sed -i '1a APACHE_ARGUMENTS=-DFOREGROUND' /usr/sbin/apache2ctl

# add bootstrap script and make it executable
COPY bootstrap.sh /etc/bootstrap.sh
RUN chown root.root /etc/bootstrap.sh
RUN chmod 744 /etc/bootstrap.sh

ENTRYPOINT ["/etc/bootstrap.sh"]
