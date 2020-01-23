# Kibana

FROM java:7-jre

# grab gosu for easy step-down from root
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture)" \
  && curl -o /usr/local/bin/gosu.asc -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture).asc" \
  && gpg --verify /usr/local/bin/gosu.asc \
  && rm /usr/local/bin/gosu.asc \
  && chmod +x /usr/local/bin/gosu

ADD ./src /

RUN chmod +x /usr/local/sbin/start.sh

# Install Kibana
RUN cd /tmp \
    && curl -O https://download.elasticsearch.org/kibana/kibana/kibana-4.0.2-linux-x64.tar.gz \
    && tar xzf kibana-*.tar.gz \
    && rm kibana-*.tar.gz \
    && mv kibana-* /opt/kibana

RUN groupadd -r kibana \
    && useradd -c "Kibana" -g kibana -M -r -s /sbin/nologin kibana


EXPOSE 5601

ENTRYPOINT ["/usr/local/sbin/start.sh"]
