# Basics
#
FROM ubuntu:14.04
MAINTAINER Van Hellsing <van.hellsing@web.de>
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -q -y git-core curl sudo xmlstarlet \
  software-properties-common python-software-properties
RUN DEBIAN_FRONTEND=noninteractive apt-get install -q -y nano
# Workaround to run nano 
ENV TERM xterm


# Install Java 7

RUN DEBIAN_FRONTEND=noninteractive apt-add-repository ppa:webupd8team/java -y
RUN apt-get update
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN DEBIAN_FRONTEND=noninteractive apt-get install oracle-java7-installer -y

# Setup volume handling
# RUN /usr/sbin/groupadd atlassian
# ADD own-volume.sh /usr/local/bin/own-volume
# RUN echo "%atlassian ALL=NOPASSWD: /usr/local/bin/own-volume" >> /etc/sudoers
RUN mkdir -p /opt/atlassian-home

# Add common script functions
ADD common.bash /usr/local/share/atlassian/common.bash
# RUN chgrp atlassian /usr/local/share/atlassian/common.bash
RUN chmod g+w /usr/local/share/atlassian/common.bash
