FROM blacklabelops/centos

USER root

RUN yum install -y \
      unzip \
      tar \
      gzip \
      wget

RUN export VIRTUALBOX_VERSION=latest && \
    mkdir -p /opt/virtualbox && \
    cd /etc/yum.repos.d/ && \
    wget http://download.virtualbox.org/virtualbox/rpm/el/virtualbox.repo && \
    yum install -y \
      dkms \
      kernel-devel && \
    yum -y groupinstall "Development Tools" && \
    if  [ "${VIRTUALBOX_VERSION}" = "latest" ]; \
      then yum install -y VirtualBox-5.0 ; \
      else yum install -y VirtualBox-5.0-${VIRTUALBOX_VERSION} ; \
    fi && \
    yum clean all && rm -rf /var/cache/yum/* && rm -rf /tmp/*
