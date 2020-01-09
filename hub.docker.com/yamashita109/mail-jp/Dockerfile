FROM yamashita109/base-jp:centos72trad

MAINTAINER yamashita109

RUN yum -y update \
    && yum -y install postfix \
    && yum clean all \
    && rm -rf /var/cache/yum/*;

EXPOSE 25
EXPOSE 465
EXPOSE 587
