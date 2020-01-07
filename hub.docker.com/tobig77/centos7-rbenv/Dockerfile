FROM centos:centos7

MAINTAINER Tobias Gerschner <tobias.gerschner@gmail.com>

ENV RUBY_VERSION 2.4.1
ENV JRUBY_VERSION 9.1.12.0
ENV RBENV_USER developer
ENV WORKDIR /opt/source

RUN yum -y install --setopt=tsflags=nodocs epel-release && \
    yum -y update && \
    yum -y install \
    bzip2 \
    gcc-c++ \
    gcc \
    git-core \
    java-1.8.0-openjdk \
    less \
    make \
    openssl-devel \
    readline-devel \
    unzip \
    wget \
    which \
    zlib-devel \
    postgresql-devel \
    mariadb-devel \
    sqlite-devel \
    && yum clean all

RUN adduser -U -m $RBENV_USER

RUN su -lc 'git clone https://github.com/rbenv/rbenv.git ~/.rbenv && cd ~/.rbenv && src/configure && make -C src' $RBENV_USER
RUN su -lc 'echo "export PATH=$HOME/.rbenv/bin:$PATH" >> ~/.bash_profile' $RBENV_USER
RUN su -c "echo 'eval \"\$(rbenv init -)\"' >> ~/.bash_profile" $RBENV_USER
RUN su -lc 'git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build' $RBENV_USER

RUN su -lc 'echo "install: --no-document" > ~/.gemrc' $RBENV_USER
RUN su -lc 'echo "update: --no-document" >> ~/.gemrc' $RBENV_USER

RUN su -lc "rbenv install $RUBY_VERSION" $RBENV_USER
RUN su -lc "rbenv install jruby-$JRUBY_VERSION ||:" $RBENV_USER
RUN su -lc "rbenv shell $RUBY_VERSION && gem install bundler" $RBENV_USER
RUN su -lc "rbenv shell jruby-$JRUBY_VERSION && gem install bundler" $RBENV_USER

EXPOSE 3000

CMD [ "/bin/su", "--login", "developer" ]
