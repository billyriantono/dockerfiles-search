# a base docker to run a minimal set of tools
FROM centos:latest
MAINTAINER Luciano Coutinho <lucianocoutinho@live.com>
LABEL version="0.4"
LABEL description="A container with a minimal set of tools."

ENV LANG en_US.utf8

ENV EPEL_URL "https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm"

# NOTE: not sure if this package is really needed:
# binutils \

ENV YUM_INSTALL_RPMS " \
  bash-completion \
  bind-utils \
  bzip2 \
  curl \
  crypto-utils \
  gdbm \
  gzip \
  iproute \
  man \
  net-tools \
  openssl \
  tar \
  tcpdump \
  telnet \
  unzip \
  screen \
  sudo \
  tmux \
  vim-enhanced \
  xz \
  zsh \
"
ENV YUM_INSTALL_RPMS_DEVEL " \
  autoconf \
  automake \
  bison \
  cscope \
  gcc \
  gcc-c++ \
  gdbm-devel \
  git \
  libcurl-devel \
  libffi-devel \
  libtool \
  libxml2-devel \
  libxslt-devel \
  libyaml-devel \
  make \
  openssl-devel \
  patch \
  pcre-devel \
  postgresql-devel \
  readline-devel \
  sqlite-devel \
  zlib-devel \
"

VOLUME /run /tmp

# Copy the basic custom envirnment settings. Of course is not good to
# do this for all the system but as this is just a docker container for
# a very specific purpose I'll do this here for a while.
COPY etc-bashrc /etc/bashrc
COPY etc-zshrc /etc/zshrc
COPY etc-screenrc /etc/screenrc
COPY etc-tmux.conf /etc/tmux.conf
COPY etc-vimrc /etc/vimrc
COPY etc-psqlrc /etc/psqlrc
COPY install-ruby.sh /tmp/install-ruby.sh

RUN set -x \
  && echo " * set yum to install docs..." \
  && sed -i 's/^tsflags=nodocs//' /etc/yum.conf \
  && echo " * install epel..." \
  && rpm -ivh ${EPEL_URL} \
  && echo " * cleanup and update system packages..." \
  && yum clean all \
  && yum update -y \
  && echo " * install all needed packages..." \
  && yum install -y ${YUM_INSTALL_RPMS} ${YUM_INSTALL_RPMS_DEVEL} \
  && echo " * add a local user 'luciano'..." \
  && adduser -s /bin/zsh -c 'Luciano Coutinho' luciano \
  && echo 'luciano        ALL=(ALL)       NOPASSWD: ALL' >> /etc/sudoers \
  && su - luciano -c 'git clone https://github.com/lucianocoutinho/dotfiles \
     && (cd dotfiles ; make install) && rm -rf dotfiles' \
  && echo ' * installing ruby' \
  && chown luciano.luciano /home/luciano/.zshrc \
  && su - luciano -c 'zsh /tmp/install-ruby.sh' \
  && rm -f /tmp/install-ruby.sh \
  && echo ' * done!'

# EOF
