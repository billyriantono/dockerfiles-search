FROM fedora:21
MAINTAINER Bryce Gibson "bryce.gibson@unico.com.au"

ENV FPM_VERSION 1.3.3

RUN yum install -y rpm-build ruby rubygems ruby-devel make gcc && \
    gem install --bindir /usr/bin -v ${FPM_VERSION} fpm && \
    yum clean all

WORKDIR /workdir

ENTRYPOINT [ "/usr/bin/fpm" ]
