FROM phusion/baseimage


EXPOSE 8300 8301 8301/udp 8302 8302/udp 8400 8500 8600/udp

RUN apt-get update && apt-get install wget zip unzip && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget https://dl.bintray.com/mitchellh/consul/0.5.2_linux_amd64.zip -O /tmp/consul.zip \
 && unzip /tmp/consul.zip \
 && rm /tmp/consul.zip \
 && mv /consul /usr/bin/consul \
 && wget https://dl.bintray.com/mitchellh/consul/0.5.2_web_ui.zip -O /tmp/consul_webui.zip \
 && unzip /tmp/consul_webui.zip \
 && mv /dist /webui \
 && rm /tmp/consul_webui.zip \ 
 && mkdir /config \ 
 && mkdir /data 

CMD /usr/bin/consul agent -config-dir /config
