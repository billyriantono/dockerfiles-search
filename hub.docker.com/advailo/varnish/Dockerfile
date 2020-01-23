FROM centos:centos7

COPY varnish.repo /etc/yum.repos.d/varnish.repo

RUN yum update -y && \
  yum install -y epel-release pygpgme yum-utils && \
  yum install -y varnish varnish-devel && \
  yum install -y git automake libtool libmaxminddb-devel python-docutils make && \

  cd /tmp/ && \

  git clone https://github.com/fgsch/libvmod-geoip2.git && \
  cd libvmod-geoip2 && \
  git submodule update --init --recursive && \
  ./autogen.sh && \
  ./configure && \
  make && \
  make install

ADD start.sh /start.sh

ENV VCL_CONFIG      /etc/varnish/default.vcl
ENV CACHE_SIZE      64m

CMD /start.sh
EXPOSE 80
