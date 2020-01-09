FROM centos:7.4.1708

MAINTAINER kiop <nick028@foxmail.com>

# set timezone
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo 'Asia/Shanghai' >/etc/timezone

RUN yum clean all; \
    (cd /lib/systemd/system/sysinit.target.wants/; for i in *; \
    do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /lib/systemd/system/multi-user.target.wants/*;\
    rm -f /etc/systemd/system/*.wants/*;\
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*;\
    rm -f /lib/systemd/system/anaconda.target.wants/*;

VOLUME [ "/sys/fs/cgroup" ]

# install
RUN \
    yum -y install epel-release ; \
    yum -y install \
    ### install nodejs  -> npm first
    nodejs \
    ## install systemd
    systemd \
    ## install redis
    redis \
    # install ssh
    passwd openssl openssh-server \
    ## add common tools
    htop vim \
    ## install qmpq pre-reqs
    ## add swoole prerequist
    gcc gcc-c++ glibc-headers wget gzip bzip2 openssl-devel \
    nghttp2 libnghttp2-devel git \
    ## add suprevisor
    supervisor unzip \
    ## add samba
    samba samba-client samba-common \
    ## install mysql server first
    mysql-community-server \
    wget make autoconf libxml2 libxml2-devel \
    openssl openssl-devel curl curl-devel \
    ## install apache
    httpd httpd-devel &&\
    ## clear cache
    rm -rf /var/cache/yum/*

## install gulp
RUN \
    npm config set registry https://registry.npm.taobao.org; \
    # add user group for apache
    useradd www ; \
    ## config ssh
    ssh-keygen -q -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key -N '' \
    && ssh-keygen -q -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key -N '' \
    && ssh-keygen -t dsa -f /etc/ssh/ssh_host_ed25519_key  -N '' \
    && sed -i "s/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config \
    && sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config; \
    ## set root password
    echo root:1|chpasswd;

ADD ./files/ /

## set service auto start
RUN \
    systemctl enable sshd;\
    systemctl enable supervisord


WORKDIR /root

CMD ["/usr/sbin/init"]

EXPOSE 9000
EXPOSE 9001
EXPOSE 9002
