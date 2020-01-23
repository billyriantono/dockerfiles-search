FROM debian:wheezy

RUN cd /tmp \
 && apt-get update \
 && apt-get -y install curl \
 && curl -O https://download.elasticsearch.org/kibana/kibana/kibana-4.0.2-linux-x64.tar.gz \
 && tar xzf kibana-*.tar.gz \
 && rm kibana-*.tar.gz \
 && mv kibana-* /opt/kibana \
 && groupadd -r kibana \
 && useradd -c "Kibana" -g kibana -M -r kibana \
 && apt-get purge -y --auto-remove curl \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD ./kibana /usr/local/bin/kibana

EXPOSE 5601

CMD ["/usr/local/bin/kibana"]