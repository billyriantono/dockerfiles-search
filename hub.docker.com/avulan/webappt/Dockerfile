FROM centos:centos7
MAINTAINER The CentOS Project <cloud-ops@centos.org>
RUN yum update -y && yum clean all
RUN yum reinstall -y glibc-common

ADD assets/i18n.sh /opt/i18n.sh
RUN /bin/bash -c 'chmod +x /opt/i18n.sh'
RUN /opt/./i18n.sh

RUN localedef -i ru_RU -f UTF-8 ru_RU.UTF-8

ENV container=docker
ENV LANG ru_RU.utf8
ENV LANGUAGE ru_RU:ru
ENV LC_ALL ru_RU.utf8

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN yum -y install rsyslog

RUN systemctl enable rsyslog.service

ADD assets/init.sh /opt/init.sh
RUN /bin/bash -c 'chmod +x /opt/init.sh'

CMD ["sh", "-c", "/opt/init.sh"]