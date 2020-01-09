FROM amazonlinux:1

ENV LANG=en_US.utf-8
ENV LC_ALL=en_US.utf-8

RUN yum -y install python36 python36-devel python36-virtualenv \
    aws-cli \
    zip unzip \
    git docker vim jq \
    openldap-devel gcc-c++ \
    && yum clean all \
    && pip-3.6 install --no-cache-dir awscli pipenv
