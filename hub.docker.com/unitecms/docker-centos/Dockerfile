#
# Centos Base image
#

FROM centos:7

# run updates
RUN yum -y update

ENV SUMMARY="Centos Base image"	\
    DESCRIPTION="Centos Base image"

LABEL summary="$SUMMARY" \
      description="$DESCRIPTION" \
      io.k8s.description="$DESCRIPTION" \
      io.k8s.display-name="Centos Base image" \
      name="unitecms/docker-centos" \
      version="1" \
      release="1" \
      maintainer="www.unitecms.io"

# Install some basic packages
RUN INSTALL_PKGS="tar findutils wget patch curl zip unzip git" && \     
    yum install -y --setopt=tsflags=nodocs $INSTALL_PKGS && \     
    rpm -V $INSTALL_PKGS && \     
    yum clean all && \
    rm -rf /var/cache/yum

COPY ./root/ /

# set correct timezone
RUN cp -f /usr/share/zoneinfo/Europe/Vienna /etc/localtime