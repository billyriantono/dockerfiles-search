#
# 2019/04/24
#   CentOS 6.7 + epel,remi,rpmforge
#	anyenv
#

FROM centos:6
MAINTAINER tamashiro

# update yum
RUN yum update -y && \
    yum clean all

RUN yum install -y git gcc make openssh-server openssh-clients sudo tar unzip which && \
    yum clean all

## libraries
RUN yum install -y bzip2-devel zlib-devel openssl-devel sqlite-devel ncurses-devel readline-devel tk-devel && \
    yum clean all

# initialize for ssh
RUN sed -i '/pam_loginuid\.so/s/required/optional/' /etc/pam.d/sshd
RUN /sbin/service sshd start
RUN /sbin/service sshd stop

# create login user
RUN useradd -d /home/dev -m -s /bin/bash dev
RUN echo dev:dev | chpasswd
RUN echo 'dev ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# timezone
RUN cp -p /usr/share/zoneinfo/Japan /etc/localtime

USER dev
RUN git clone https://github.com/riywo/anyenv ~/.anyenv

RUN mkdir -p $HOME/.anyenv/plugins
RUN git clone https://github.com/znz/anyenv-update.git $HOME/.anyenv/plugins/anyenv-update

RUN echo 'export PATH="$HOME/.anyenv/bin:$PATH"' >> ~/.bashrc
RUN echo 'eval "$(anyenv init -)"' >> ~/.bashrc
RUN exec $SHELL -l
RUN $HOME/.anyenv/bin/anyenv install --force-init


EXPOSE 22

USER root
CMD ["/usr/sbin/sshd","-D"]
