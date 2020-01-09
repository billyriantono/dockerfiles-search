FROM centos:7
MAINTAINER Solitudo, LLC <info@solitudo.co.jp>

# System
RUN localedef -f UTF-8 -i ja_JP ja_JP.utf8 \
  && sed -i -e 's/^LANG=.*/LANG=ja_JP.utf8/' /etc/locale.conf \
  && sed -i -e '/override_install_langs/s/$/,ja_JP.utf8/g' /etc/yum.conf \
  && sed -i -e 's/^tsflags=nodocs/#\0/' /etc/yum.conf \
  && ln -snf /usr/share/zoneinfo/Japan /etc/localtime \
  && passwd -d root \
  && passwd -l root \
  && yum -y update \
  && yum -y install @core @base epel-release \
  && yum -y install zsh tmux vim-enhanced git gcc gcc-c++ patch automake autoconf glibc-static

# SSH
RUN /sbin/sshd-keygen

# Docker
RUN yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo \
  && yum -y install docker-ce \
  && curl -sSL "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
  && chmod +x /usr/local/bin/docker-compose

# Node.js
RUN curl -sSL https://rpm.nodesource.com/setup_8.x | bash - \
  && yum -y install nodejs \
  && npm install -g npm c9

# Cloud9
RUN git clone --depth 1 https://github.com/c9/core.git /usr/local/src/c9sdk \
  && cd /usr/local/src/c9sdk \
  && npm install --production \
  && npm install pty.js sqlite3 sequelize coffee less sass typescript stylus pug \
  && git checkout HEAD -- node_modules

# User
RUN useradd -m -u 1000 -s /bin/zsh user \
  && passwd -d user \
  && echo 'user ALL=(ALL) ALL' >/etc/sudoers.d/user
RUN sudo -Hu user mkdir -p /home/user/.c9/tmp \
  && curl -L https://raw.githubusercontent.com/c9/install/master/install.sh | sudo -Hu user bash

# Tools
RUN yum -y install nmap-ncat jq
RUN yum -y clean all && rm -rf /var/cache/yum /tmp/*

# Files
ADD bin/ /usr/local/bin/
ADD etc/ /etc/
ADD c9sdk/ /usr/local/src/c9sdk/

ENTRYPOINT ["/bin/sh", "/usr/local/bin/entrypoint.sh"]
