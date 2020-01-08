FROM centos:7
MAINTAINER "D0han" <d0hanzibi@gmail.com>
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN yum groupinstall -y "Development Tools"
RUN yum install -y python python-devel wget libffi libffi-devel openssl-devel
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install ansible==2.2.0.0

VOLUME [ "/sys/fs/cgroup", "/run", "/tmp" ]
CMD ["/usr/sbin/init"]

