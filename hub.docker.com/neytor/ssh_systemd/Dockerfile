FROM centos

MAINTAINER Yonier Gómez yonieer13@gmail.com

LABEL ssh: v1

RUN yum -y install openssh openssh-server openssh-clients openssl-libs \ 
    net-tools bind-utils vim sudo

ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]

ENV user=labo \
    password=labo \
    passroot=labo

RUN useradd $user && echo $password | passwd --stdin $user && \
    echo $passroot | passwd --stdin root && \
    echo "$user ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/$user && \
    ssh-keygen -A

RUN systemctl enable sshd

EXPOSE 22 80

CMD ["/usr/sbin/init"]
