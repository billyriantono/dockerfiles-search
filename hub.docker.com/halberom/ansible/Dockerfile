FROM centos:centos7

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /lib/systemd/system/multi-user.target.wants/*; \
    rm -f /etc/systemd/system/*.wants/*; \
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*; \
    rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN yum clean all && \
    yum -y install epel-release && \
    yum -y install \
      bzip2 \
      cronie \
      fakesystemd \
      file \
      gcc \
      git \
      iproute \
      libffi \
      libffi-devel \
      make \
      python-devel \
      python-httplib2 \
      python-keyczar \
      python-lxml \
      python-paramiko \
      python-passlib \
      python-pip \
      python-setuptools \
      sudo \
      unzip \
      which \
      && \
    pip install --upgrade pip && \
    pip install ansible netaddr && \
    yum -y remove \
      gcc \
      python-devel \
      && \
    yum clean all

RUN /usr/bin/sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers && \
    mkdir /etc/ansible/ && \
    /usr/bin/echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts
VOLUME /sys/fs/cgroup /run /tmp
ENV container=docker
CMD ["/usr/sbin/init"]
