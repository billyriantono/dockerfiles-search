# === Base Image ===
# 注意此處的 AS
FROM ruby:2.4.1 AS passenger_ruby
MAINTAINER white <a500667337@gmail.com>

# Default Environment
# 在這邊設定 相關軟體的版本
ENV NGINX_VERSION 1.12.2
ENV PASSENGER_VERSION 6.0.2
RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list
# Requirement
RUN apt-get update && apt-get install -y libmagick++-dev libmariadb-client-lgpl-dev libpcap-dev libssl-dev

# シェルスクリプトとしてbashを利用
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
# yarnパッケージ管理ツールインストール
RUN apt-get update && apt-get install -y curl apt-transport-https wget && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn

# Node.jsをインストール
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install nodejs

# 中文字型
RUN apt-get install -y xfonts-wqy
RUN apt-get install -y ttf-wqy-zenhei
RUN apt-get install -y fonts-arphic-ukai

# 以指定的安裝 Passenger Gem
RUN gem install passenger -v $PASSENGER_VERSION
# 指定 Passenger 編譯 Nginx Extension
# 在這邊使用 passenger-config about root 取得 Passenger 的 root 目錄
RUN cd `passenger-config about root` && rake nginx
# 以前述變數指定版本 Checkout Nginx Source Code
RUN cd /tmp && wget https://nginx.org/download/nginx-$NGINX_VERSION.tar.gz && tar -zxvf nginx-$NGINX_VERSION.tar.gz
# 編譯 Nginx 並加入 Passenger 與 upload module extension
RUN cd /tmp/nginx-$NGINX_VERSION && ./configure --with-http_v2_module --with-http_ssl_module --add-module="`passenger-config about root`/src/nginx_module" --with-http_gzip_static_module && make && make install

# === Rails Application ===
# 使用 multi-stage 方式
# From 剛才的 AS
FROM passenger_ruby

# 重要！
ENV LC_ALL C.UTF-8
# 指定時區，否則會用 GMT
ENV TZ Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# 設定一個程式起始的目錄
ENV APP_HOME /usr/src/app
RUN mkdir -p $APP_HOME

ENV RAILS_ENV production
ENV RAKE_ENV production
ENV BUNDLE_JOBS=30