FROM centos:7
MAINTAINER OKUMURA Takahiro <hfm.garden@gmail.com>

ADD build_config.rb /tmp/build_config.rb

RUN yum -y -q install make gcc git rubygems openssl-devel curl wget bison mariadb-devel which ruby-devel \
  && gem i -N json_pure \
  && gem update --system 2.6.1 \
  && gem i -N bundler -v 1.12.5 \
  && gem i -N rake \
  && git clone --depth=1 https://github.com/matsumoto-r/ngx_mruby.git \
  && cp /tmp/build_config.rb ngx_mruby/build_config.rb \
  && cd ngx_mruby \
  && sh build.sh \
  && cp mruby/bin/mruby /usr/local/bin
