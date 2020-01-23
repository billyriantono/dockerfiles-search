FROM centos:6

RUN yum -y install epel-release vim telnet wget man yumdownloader

RUN curl https://bootstrap.pypa.io/get-pip.py | python && pip install awscli

COPY google-cloud-sdk.repo /etc/yum.repos.d/

RUN yum -y install google-cloud-sdk

