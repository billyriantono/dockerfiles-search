FROM centos:latest

MAINTAINER zzzshanghai

ENV INSTALL_DIR=/root/shadowsocks

RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-* && \
    yum clean all && \
    yum makecache && \
    yum update -y && \
    yum install -y m2crypto python-setuptools git curl iptables-devel && \
    easy_install pip && pip install shadowsocks cymysql

RUN git clone -b manyuser https://github.com/andy501336/ss-mod-manyuser.git $INSTALL_DIR

WORKDIR /root/shadowsocks

RUN python setup.py install

EXPOSE 10086

ENV DNS_ADDR    8.8.8.8
ENV DNS_ADDR_2  8.8.4.4

CMD bash run.sh
