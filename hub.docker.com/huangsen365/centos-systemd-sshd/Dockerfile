FROM centos/systemd

MAINTAINER "Your Name" <you@example.com>

RUN sed -i 's/tsflags=nodocs/\#tsflags=nodocs/g' /etc/yum.conf
RUN echo "ip_resolve=4" >> /etc/yum.conf
RUN yum -y update
RUN yum -y install epel-release
RUN yum -y install man-pages man-db man centos-release-scl htop iftop tmux unzip wget python-pip bind-utils

RUN echo "export HISTSIZE=999999999" >> /etc/bashrc
RUN echo "export HISTTIMEFORMAT=\"%F %T \"" >> /etc/bashrc


RUN rm -rf /etc/localtime
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN yum makecache fast
RUN yum -y install openssh-clients openssh-server \
        iproute \
        net-tools \
        nmap \
        vim-enhanced \
        rh-python36 \
        telnet \
        bind

COPY vimrc_append_conf.txt /tmp
RUN cat /tmp/vimrc_append_conf.txt >> /etc/vimrc

RUN systemctl enable sshd.service

EXPOSE 22

CMD ["/usr/sbin/init"]
