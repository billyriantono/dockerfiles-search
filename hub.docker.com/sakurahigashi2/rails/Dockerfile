FROM centos:7

# rootのパスワード設定
RUN echo "root" | passwd --stdin root

# システム時刻を東京に変更
RUN unlink /etc/localtime;ln -s /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# 必須パッケージインストール
RUN yum -y update
RUN yum -y install git bzip2 gcc make openssh-server iputils iproute which openssl-devel readline-devel zlib-devel sqlite-devel postgresql-devel mysql-devel

# 環境変数設定
ENV RBENV_ROOT /usr/local/rbenv
ENV RUBY_V 2.5.0
ENV RAILS_V 5.1.4
ENV NVM_ROOT /usr/local/nvm
ENV NODE_V 9.7.1

# パス設定
ENV PATH $RBENV_ROOT/bin:$PATH
ENV PATH $RBENV_ROOT/shims:$PATH

# rbenv経由でrubyのインストール
RUN git clone https://github.com/sstephenson/rbenv.git $RBENV_ROOT
RUN eval "$(rbenv init -)"
RUN git clone git://github.com/sstephenson/ruby-build.git $RBENV_ROOT/plugins/ruby-build && \
    cd $RBENV_ROOT/plugins/ruby-build && ./install.sh && rm -f ./install.sh && cd ~
RUN rbenv install $RUBY_V && \
    rbenv rehash && \
    rbenv global $RUBY_V

# Railsのインストール
RUN gem install rails --version=$RAILS_V

# nvm + node.js + npm + yarnインストール
RUN git clone git://github.com/creationix/nvm.git $NVM_ROOT
RUN chmod 755 $NVM_ROOT/nvm.sh
RUN source $NVM_ROOT/nvm.sh && \
    nvm install $NODE_V && \
    nvm alias default $NODE_V && \
    npm install -g yarn
RUN touch /etc/profile.d/setup.sh && \
    echo 'source $NVM_ROOT/nvm.sh' >> /etc/profile.d/setup.sh

CMD ["/sbin/init"]
