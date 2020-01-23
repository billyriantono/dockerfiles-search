FROM telegraf:1.0.1-alpine

RUN apk add --update curl unzip && \
    rm -rf /var/cache/apk/*

RUN curl https://releases.hashicorp.com/consul/0.6.4/consul_0.6.4_linux_amd64.zip > /tmp/consul.zip && unzip /tmp/consul.zip
RUN curl -L https://github.com/kreuzwerker/envplate/releases/download/v0.0.8/ep-linux -o /usr/local/bin/ep && chmod +x /usr/local/bin/ep

RUN mv consul /usr/local/bin/
RUN mkdir -p /etc/consul/conf.d
ADD consul.json /etc/consul/consul.json.tpl

ENV CONSUL_HOST consul
ADD consul.sh /root/consul.sh

ENTRYPOINT ["/root/consul.sh"]

