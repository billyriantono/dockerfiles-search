# centos7 docker
#

FROM centos:centos7
MAINTAINER test

# timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# locale
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8

# epel
RUN rpm --import http://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7
RUN rpm -ivh http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

# remi
RUN rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm



RUN yum -y update

# user
RUN useradd app
RUN yum -y install sudo
RUN echo "app ALL=(ALL) ALL" > /etc/sudoers.d/app
RUN echo 'app:app' | chpasswd
RUN echo "export LANG=ja_JP.UTF-8" >> /home/app/.bashrc
RUN mkdir /home/app/.ssh
RUN chmod 700 /home/app/.ssh
RUN touch /home/app/.ssh/config
RUN chmod 600 /home/app/.ssh/config
RUN chown -R app:app /home/app/.ssh

# sendmail
# RUN yum -y install sendmail

# dev package
RUN yum install -y bind-utils tar make libxml2-devel libxslt-devel libcurl-devel ImageMagick-devel zlib-devel libffi-devel wget httpd readline readline-devel sqlite sqlite-devel lua-devel ncurses-devel lua-devel lynx ctags

# ssh
RUN yum -y install openssh-server
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''
RUN ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key -N ''

# devtools
RUN yum install -y gcc gcc-c++ zsh git
RUN chsh app -s /bin/zsh

# dotfiles
RUN cd /home/app && git clone https://github.com/f96q/dotfiles.git
RUN chown -R app:app /home/app/dotfiles
RUN su - app -c 'cd /home/app/dotfiles && sh setup.sh'

# ruby
#RUN yum remove ruby
#RUN yum -y install libyaml openssl openssl-devel

# rbenv
#RUN git clone https://github.com/sstephenson/rbenv.git ${HOME}/.rbenv
#RUN git clone https://github.com/sstephenson/ruby-build.git ${HOME}/.rbenv/plugins/ruby-build
#RUN .${HOME}/.rbenv/plugins/ruby-build/install.sh
#ENV PATH ${HOME}/.rbenv/bin:$PATH
#RUN echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh
#RUN echo 'eval "$(rbenv init -)"' >> .bashrc

#RUN git clone https://github.com/sstephenson/rbenv.git ${HOME}/.rbenv
#RUN git clone https://github.com/sstephenson/ruby-build.git ${HOME}/.rbenv/plugins/ruby-build
#RUN .${HOME}/.rbenv/plugins/ruby-build/install.sh
#ENV PATH ${HOME}/.rbenv/shims:${HOME}/.rbenv/bin:$PATH
#RUN echo 'export PATH=${HOME}/.rbenv/shims:${HOME}/.rbenv/bin:$PATH' >> ${HOME}/.bashrc
#RUN echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh
#RUN echo 'eval "$(rbenv init -)"' >> ${HOME}/.bashrc
#RUN source ${HOME}/.bashrc

# ruby
RUN yum install -y centos-release-scl-rh centos-release-scl
#ENV CONFIGURE_OPTS --disable-install-doc
#RUN rbenv --version
#RUN /root/.rbenv/bin/rbenv install 2.4.0
#RUN /root/.rbenv/bin/rbenv global 2.4.0
#RUN yum --enablerepo=centos-sclo-rh install -y rh-ruby24-ruby-devel

# mysql
#RUN yum install -y mysql-server
#RUN chkconfig mysqld on

#RUN git clone https://github.com/yyuu/pyenv.git ${HOME}/.pyenv

# python
#RUN echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ${HOME}/.bashrc
#RUN echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ${HOME}/.bashrc
#RUN echo 'eval "$(pyenv init -)"' >> ${HOME}/.bashrc

#RUN source ${HOME}/.bashrc
#RUN ${HOME}/.pyenv/bin/pyenv install 3.6.1

#RUN ${HOME}/.pyenv/bin/pyenv global 3.6.1
#RUN ${HOME}/.pyenv/bin/pyenv rehash

# vim
#RUN cd /tmp \
#    && git clone https://github.com/vim/vim.git \
#    && cd /tmp/vim \
#    && ./configure --with-features=huge --with-python-config-dir=/usr/lib/python2.6/config --enable-rubyinterp --enable-luainterp --enable-fail-if-missing \
#    && make \
#    && make install

# dein.vim
#RUN mkdir -p ${HOME}/.vim/dein/repos/github.com/Shougo/dein.vim
#RUN git clone https://github.com/Shougo/dein.vim.git ${HOME}/.vim/dein/repos/github.com/Shougo/dein.vim

# ruby dicts
#RUN git clone https://github.com/pocke/dicts

# vim refe
#RUN gem install refe2
#RUN bitclust setup

