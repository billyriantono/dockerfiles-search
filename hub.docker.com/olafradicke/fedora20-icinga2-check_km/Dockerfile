# DOCKER-VERSION 0.3.4
# image olafradicke/fedora20-icinga2-check_km
# Install based on Doku http://docs.icinga.org/icinga2/latest/doc/module/icinga2/chapter/getting-started

FROM fedora:20
MAINTAINER Olaf Raicke <olaf@atix.de>

ENV ICINGA2_USER icinga
ENV ICINGA2_GROUP icingacmd
ENV ICINGA2_CONFIG_FILE /etc/icinga2/icinga.cfg
ENV ICINGA2_ERROR_LOG /var/log/icinga2/error.log

ENV BUILD_DIR /tmp

ADD ./scripts/start.sh /start.sh
RUN chmod 755 /start.sh
RUN ls -lah

RUN yum -y update
RUN yum -y --setopt=tsflags=nodocs install wget
RUN yum -y --setopt=tsflags=nodocs install httpd

RUN wget http://packages.icinga.org/fedora/ICINGA-release.repo -O /etc/yum.repos.d/ICINGA-release.repo
RUN yum makecache
RUN yum -y --setopt=tsflags=nodocs install icinga2 nagios-plugins-all

RUN mkdir /var/run/icinga2/
RUN chown $ICINGA2_USER.$ICINGA2_GROUP /var/run/icinga2/

#############################

# check_mk
RUN  yum -y install --nogpgcheck  https://mathias-kettner.de/download/check_mk-agent-1.2.4p5-1.noarch.rpm

###################################################

# for password less logins
VOLUME ["/root/.ssh:/var/docker-container/root-ssh"]
VOLUME ["/var/log/:/var/docker-container/log/fedora20-icinga/"]
EXPOSE 22
EXPOSE 80

ENTRYPOINT  ["/bin/bash"]
CMD ["start.sh"]







