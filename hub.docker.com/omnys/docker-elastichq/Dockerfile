FROM nginx:latest

MAINTAINER sistemi@omnys.com

ADD https://github.com/royrusso/elasticsearch-HQ/archive/master.tar.gz /tmp/elasticsearch-HQ-master.tar.gz

RUN \
  cd /tmp && \
  tar xzf /tmp/elasticsearch-HQ-master.tar.gz && \
  mv -f /tmp/elasticsearch-HQ-master/* /usr/share/nginx/html && \
  rm -rf /tmp/elasticsearch-HQ-master*
