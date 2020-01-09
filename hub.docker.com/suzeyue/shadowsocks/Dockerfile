FROM centos:7

MAINTAINER suzeyue <suzeyue42@gmail.com>

RUN yum -y install python-setuptools && easy_install pip
RUN pip install shadowsocks

ENV SERVER_PORT 32000
ENV PASSWORD helloWorld
ENV METHOD rc4-md5

COPY entrypoint.sh /entrypoint.sh
RUN chmod 755 /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
