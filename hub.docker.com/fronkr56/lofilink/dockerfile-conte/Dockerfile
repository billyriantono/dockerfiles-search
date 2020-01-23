FROM alpine

MAINTAINER frjaraur@gmail.com

RUN apk --update --no-progress --no-cache add curl

#COPY consul /bin/consul

WORKDIR /CONSUL

ENV CONSUL_VERSION 0.6.4

RUN curl -o /CONSUL/consul_web_ui.zip -sS https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_web_ui.zip  \
&& curl -o /CONSUL/consul.zip  -sS https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip

RUN mkdir -p /CONSUL/ui \
&& unzip /CONSUL/consul_web_ui.zip -d /CONSUL/ui \
&& rm -f /CONSUL/consul_web_ui.zip \
&&  unzip /CONSUL/consul.zip -d /sbin \
&& rm -f /CONSUL/consul.zip

VOLUME /CONSUL

COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

#Server RPC
EXPOSE 8300

#Serf LAN
EXPOSE 8301 8301/udp

#Serf WAN
EXPOSE 8302 8302/udp

#CLI RPC
EXPOSE 8400

#API HTTP
EXPOSE 8500

#DNS Interface
EXPOSE 8600 8600/udp

CMD ["help"]
