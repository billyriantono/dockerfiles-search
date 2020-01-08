FROM mycongrats/centos

COPY vim.cnf /root/
COPY env.cnf /root/
COPY solarized.vim /usr/share/vim/vim74/colors/

RUN yum install -y epel-release

RUN yum install -y which cronie lsof vim zip unzip openssh-server openssh-clients \
    && yum clean all

RUN cat /root/vim.cnf >> /etc/vimrc \
    && cat /root/env.cnf >> /etc/bashrc \
    && rm -rf /root/vim.cnf /root/env.cnf \
    && sed -i '$ a export HISTTIMEFORMAT="%F %T `whoami` "' /etc/bashrc
