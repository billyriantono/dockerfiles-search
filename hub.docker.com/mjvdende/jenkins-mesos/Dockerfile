FROM jenkins
MAINTAINER mjvdende <@mjvdende>

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

USER root

#====================
# Copy mesos lib
#====================
COPY libmesos-0.24.1.so /var/lib/libmesos-0.24.1.so

USER jenkins
