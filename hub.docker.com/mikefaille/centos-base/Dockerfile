FROM centos:7
MAINTAINER michael@faille.io <michael@faille.io>

# YUM config
RUN echo "pub  4096R/F4A80EB5 2014-06-23 CentOS-7 Key (CentOS 7 Official Signing Key) <security@centos.org> Key fingerprint = 6341 AB27 53D7 8A78 A7C2  7BB1 24C6 A8A7 F4A8 0EB5" | gpg --quiet --with-fingerprint /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

# Base soft
RUN echo "installonlypkgs=procps-ng" >> /etc/yum.conf &&\
    yum install -y epel-release &&  yum install -y net-utils make wget git tar vim  python-setuptools supervisor hostname; yum clean all

ENV WORKDIR /data
RUN mkdir -p /data/persistent
WORKDIR $WORKDIR

# Supervisor
ADD conf/supervisord.conf /etc/supervisord.conf
ADD conf/supervisor-base.ini /etc/supervisord.d/base.ini

CMD ["/usr/bin/supervisord"]
