# PixelHyperlink Gerrit Server Docker
#
# VERSION               1.0.0

FROM pixelhyperlinkdockers/javajdk:v1.1.0
MAINTAINER Abhishek Salian <abhi@pixelhyperlink.com>

LABEL Description="This image contains base ubuntu os with gerrit service."
LABEL Vendor="PixelHyperlink"
LABEL Version="1.0.0"
LABEL com.pixelhyperlink.docker.apacheserver.version="1.0.0"
LABEL vendor="PixelHyperlink"
LABEL com.pixelhyperlink.docker.apacheserver.release-date="2017-08-02"
LABEL com.pixelhyperlink.docker.apacheserver.version.is-production="true"

ENV RUNLEVEL 1

# Install apache.
RUN apt-get update && \
	apt-get -y install git \
	apache2 \
	gitweb

# Expose apache.
EXPOSE 80 443 29418

VOLUME ["/var/log/apache2", "/opt/gerrit"]

RUN mkdir -p /opt/gerrit/etc /opt/gerrit/plugins

# Copy gerrit config.
COPY ./gerrit.config /opt/gerrit/etc/gerrit.config
COPY ./project.config /opt/gerrit/etc/project.config
COPY ./replication.config /opt/gerrit/etc/replication.config
COPY ./reviewers.config /opt/gerrit/etc/reviewers.config

# Copy plugins downloaded from https://gerrit-ci.gerritforge.com/view/Plugins-stable-2.14/
COPY ./plugins/2.14/ /opt/gerrit/plugins/

# Copy gerrit
COPY ./gerrit/gerrit-2.14.2.war /tmp/gerrit-2.14.2.war

# Copy apache config.
COPY ./apache2.conf /etc/apache2/apache2.conf

# Update the default apache site with the config we created.
COPY ./000-default.conf /etc/apache2/sites-enabled/000-default.conf

# Set FQDN.
COPY ./fqdn.conf /etc/apache2/conf-available/fqdn.conf

# Copy htpasswd
# http://www.htaccesstools.com/htpasswd-generator/
# or
# htpasswd /etc/apache2/gerrit.htpasswd username
COPY ./gerrit.htpasswd /etc/apache2/gerrit.htpasswd

# Copy server start up scripts
COPY ./gerrit_entrypoint.sh /opt/gerrit_entrypoint.sh

# Run startup scripts
RUN chmod 777 /opt/gerrit_entrypoint.sh

ENTRYPOINT ["/opt/gerrit_entrypoint.sh"]
