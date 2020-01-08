FROM centos:6
MAINTAINER Star Lab <support@starlab.io>

RUN mkdir /source
WORKDIR /source

# Install IUS so we can get a recent version of git
RUN yum install -y https://centos6.iuscommunity.org/ius-release.rpm && \
    yum clean all && \
    rm -rf /var/cache/yum/* /tmp/* /var/tmp/*

RUN yum install -y attr python27 python27-pip openssh openssh-clients git2u && \
    yum clean all && \
    rm -rf /var/cache/yum/* /tmp/* /var/tmp/*

# Just replace the stock (2.6) python with 2.7
RUN ln -sf $(which python2.7) $(which python)
RUN ln -s $(which pip2.7) /usr/bin/pip
