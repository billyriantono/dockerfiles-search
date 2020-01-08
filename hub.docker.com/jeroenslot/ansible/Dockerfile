FROM centos:7.6.1810

RUN yum clean all && \
    yum -y install epel-release && \
    yum -y install \
        curl \
        openssh-clients \
        PyYAML \
        python-jinja2 \
        python-httplib2 \
        python-keyczar \
        python-paramiko \
        python-setuptools \
        python-pip && \
    pip install --upgrade pip && \
    pip install ansible && \
    rm -rf /var/cache/apk/*

WORKDIR /etc/ansible