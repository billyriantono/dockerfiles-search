FROM grafana/grafana:3.1.1

RUN apt-get update && \
    apt-get -y --no-install-recommends install curl unzip ca-certificates && \
    apt-get clean && \
    curl https://releases.hashicorp.com/consul/0.6.4/consul_0.6.4_linux_amd64.zip > /tmp/consul.zip && unzip /tmp/consul.zip && \
    curl -L https://github.com/kreuzwerker/envplate/releases/download/v0.0.8/ep-linux -o /usr/local/bin/ep && chmod +x /usr/local/bin/ep && \
    rm -rf /var/lib/apt/lists/*

RUN mv consul /usr/local/bin/
RUN mkdir -p /etc/consul/conf.d
ADD consul.json /etc/consul/consul.json.tpl

ENV CONSUL_HOST consul
ADD consul.sh /root/consul.sh

ENTRYPOINT ["/root/consul.sh"]
