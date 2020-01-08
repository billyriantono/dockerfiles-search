FROM centos:6.8

ENV HOME /root
ENV PATH ${HOME}/.rbenv/bin:${PATH}:/usr/lib64/qt5/bin/
ENV RUBY_VERSION 2.3.1
ENV MYSQL_REPO_VERSION 6-5
ENV MYSQL_VERSION 56
ENV BUNDLER_VERSION 1.13.6

ENV APP_ROOT ${HOME}/project

RUN yum -y install epel-release
RUN yum -y install \
    git \
    gcc \
    openssl-devel \
    readline-devel \
    zlib-devel \
    http://dev.mysql.com/get/mysql-community-release-el${MYSQL_REPO_VERSION}.noarch.rpm \
    yum-utils \
    sqlite-devel \
    ImageMagick-devel \
    patch \
    gcc-c++ \
    qt5-qtwebkit-devel

RUN git clone https://github.com/sstephenson/rbenv.git ~/.rbenv \
    && git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
RUN echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh
RUN echo 'eval "$(rbenv init -)"' >> ~/.bashrc
RUN rbenv install ${RUBY_VERSION}
RUN rbenv global ${RUBY_VERSION}

RUN yum-config-manager --disable mysql*-community*
RUN yum -y --enablerepo=mysql${MYSQL_VERSION}-community install \
    mysql-community-server \
    mysql-community-devel
RUN chkconfig mysqld on

RUN echo 'gem: --no-rdoc --no-ri' >> ~/.gemrc
RUN bash -l -c 'gem install bundler -v ${BUNDLER_VERSION}'

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.7/install.sh | bash
RUN bash -l -c 'nvm install node'
