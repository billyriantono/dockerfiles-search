FROM        alpine:3.4
MAINTAINER  Hortonworks

ENV CONSUL_TEMPLATE_VERSION 0.16.0
ENV PROMETHEUS_VERSION 1.4.1

RUN apk add --update tar curl bash ca-certificates openssl && update-ca-certificates

# Add consul-template
RUN wget https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip -O /tmp/consul-template.zip
RUN unzip /tmp/consul-template.zip -d /usr/local/bin

# Add prometheus
RUN wget https://github.com/prometheus/prometheus/releases/download/v${PROMETHEUS_VERSION}/prometheus-${PROMETHEUS_VERSION}.linux-amd64.tar.gz -O - | tar -xzC /tmp --strip-components=1 -f -
RUN mv /tmp/prometheus /usr/local/bin/prometheus
RUN mv /tmp/promtool  /usr/local/bin/promtool

RUN mkdir -p /etc/prometheus/rules
RUN mv /tmp/prometheus.yml /etc/prometheus/prometheus.yml

RUN mkdir /usr/share/prometheus
RUN mv /tmp/console_libraries /usr/share/prometheus
RUN mv /tmp/consoles /usr/share/prometheus

RUN rm -rf /tmp/* /var/cache/apk/*

ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ADD prometheus.yml.ctmpl /etc/prometheus/prometheus.yml.ctmpl
ADD alerting_rules.ctmpl /etc/prometheus/alerting_rules.ctmpl
ADD aggregation_rules.ctmpl /etc/prometheus/aggregation_rules.ctmpl

ENTRYPOINT [ "/entrypoint.sh" ]
EXPOSE     9090
