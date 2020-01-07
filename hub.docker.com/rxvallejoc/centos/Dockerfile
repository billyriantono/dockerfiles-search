FROM centos:7

RUN yum -y install openssh

RUN mkdir /root/.ssh && chmod 700 /root/.ssh

COPY kitchen_rsa  /root/.ssh/
COPY kitchen_rsa.pub  /root/.ssh/
RUN cat /root/.ssh/kitchen_rsa.pub >> /root/.ssh/authorized_keys
RUN chmod 600 /root/.ssh/kitchen_rsa

RUN yum -y install openssh-server sudo && \
    ssh-keygen -t rsa -N '' -f /etc/ssh/ssh_host_rsa_key

RUN sed -ri 's/^session\s+required\s+pam_loginuid.so$/session optional pam_loginuid.so/' /etc/pam.d/sshd && \
    sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -ri 's/^#?PubkeyAuthentication\s+.*/PubkeyAuthentication yes/' /etc/ssh/sshd_config && \
    sed -ri 's/requiretty/!requiretty/' /etc/sudoers && \
    echo 'root:docker.io' | chpasswd

RUN sed -ri 's/langs=en_US.UTF-8/langs=en_US.utf8/' /etc/yum.conf && \
       yum reinstall -y glibc-common

RUN yum -y install nc net-tools iptables

ENV container docker

RUN yum -y update; \
    yum -y install systemd; yum clean all;

RUN cd /lib/systemd/system/sysinit.target.wants/; ls -1 | grep -v systemd-tmpfiles-setup.service | xargs rm; \
      rm -f /etc/systemd/system/*.wants/*;\
      rm -f /lib/systemd/system/local-fs.target.wants/*; \
      rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
      rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
      rm -f /lib/systemd/system/basic.target.wants/*;\
      rm -f /lib/systemd/system/anaconda.target.wants/*;\
      systemctl preset sshd;

EXPOSE 22

VOLUME [ "/sys/fs/cgroup" ]
CMD [ "/usr/sbin/init" ]
