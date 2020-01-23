FROM debian:stretch
MAINTAINER eric von zee <eric@base10.org>

#Supervisor config
ADD supervisord.conf /etc/supervisord.conf

# Install Salt
ADD bootstrap.sh /tmp/bootstrap.sh
RUN /bin/bash /tmp/bootstrap.sh

# Volumes
VOLUME ["/etc/salt/pki","/var/cache/salt","/var/log/salt","/etc/salt/master.d","/srv/salt","/srv/pillar"]

# Ports.
EXPOSE 4505 4506 5417

# Run Command
CMD ["/usr/bin/supervisord","-c","/etc/supervisord.conf"]
