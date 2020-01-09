# Base CentOS 7 with a few perks
# Includes epel repo for local build

FROM centos:7.1.1503

MAINTAINER Blaz Zupanc

RUN yum update -y && yum install net-tools tar wget unzip -y && yum clean all && \
    yum install epel-release -y && \
    yum repolist && \
    yum install pwgen -y && \
    yum clean all

ENV container docker

RUN yum -y swap -- remove fakesystemd -- install systemd systemd-libs; yum clean all; \
  (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
  rm -f /lib/systemd/system/multi-user.target.wants/*;\
  rm -f /etc/systemd/system/*.wants/*;\
  rm -f /lib/systemd/system/local-fs.target.wants/*; \
  rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
  rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
  rm -f /lib/systemd/system/basic.target.wants/*;\
  rm -f /lib/systemd/system/anaconda.target.wants/*;

VOLUME [ "/sys/fs/cgroup" ]

CMD ["/usr/sbin/init"]

WORKDIR /opt

RUN yum install -y openssh-server openssh-clients passwd sudo && \
    yum clean all

ENV USERPWD secret
ADD removekeys.sh /opt/removekeys.sh

RUN useradd -u 5001 -G users -m user && \
    echo "$USERPWD" | passwd user --stdin && \
    chmod +x /opt/removekeys.sh && \
    /usr/bin/ssh-keygen -A -v && \
    sed -i '/^session.*pam_loginuid.so/s/^session/# session/' /etc/pam.d/sshd && \
    sed -i 's/Defaults.*requiretty/#Defaults requiretty/g' /etc/sudoers && \
    rm /usr/lib/tmpfiles.d/systemd-nologin.conf

# passwordless sudo
ADD user /etc/sudoers.d/user

EXPOSE 22

CMD ["/usr/sbin/init"]
