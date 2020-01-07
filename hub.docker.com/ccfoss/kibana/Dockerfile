FROM ccfoss/alpine-consul
MAINTAINER Chaitanya Akkineni cakkinen@cisco.com

ENV GOSU_VERSION 1.10
ENV GOSU_URL https://github.com/tianon/gosu/releases/download
ENV KIBANA_VERSION 5.0.0

RUN apk add --update bash nodejs gosu@testing && \
    rm -rf /var/cache/apk/*

RUN apk add --update wget ca-certificates &&\
  cd /tmp  &&\
  wget -O kibana.tar.gz https://artifacts.elastic.co/downloads/kibana/kibana-5.0.0-linux-x86_64.tar.gz  &&\
  tar -xzf kibana.tar.gz  &&\
  mv kibana-$KIBANA_VERSION-linux-x86_64 /usr/local/kibana  &&\
  adduser -DH -s /sbin/nologin kibana  &&\
  rm /usr/local/kibana/node/bin/node &&\
  rm /usr/local/kibana/node/bin/npm &&\
  ln -s /usr/bin/node /usr/local/kibana/node/bin/node &&\
  ln -s /usr/bin/npm /usr/local/kibana/node/bin/npm &&\
  chown -R kibana:kibana /usr/local/kibana  &&\
  rm -rf /tmp/*  &&\
  rm -rf /var/cache/apk/*

RUN /usr/local/kibana/bin/kibana-plugin install x-pack

WORKDIR /usr/local/kibana
ENV PATH /usr/local/kibana/bin:$PATH

EXPOSE 5601

ADD kibana.yml.ctmpl /usr/local/kibana/config/
ADD consul-template.hcl /etc/consul.d/
CMD ["kibana"]