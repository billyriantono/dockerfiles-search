FROM amazonlinux:2018.03
RUN yum upgrade -y \
    && yum -y install python36 python36-virtualenv python36-pip zip \
    && rm -rf /var/cache/yum/* \
    && yum clean all

RUN ln -s /usr/bin/pip-3.6 /usr/bin/pip3 \
    && pip3 install --upgrade pip
