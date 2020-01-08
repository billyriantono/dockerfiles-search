#
# Kibana Dockerfile
#
# https://github.com/pasangsherpa/docker-kibana
#

# Pull base image.
FROM java:7-jre

MAINTAINER Pasang Sherpa "https://github.com/pasangsherpa"

ENV KIBANA_PKG_NAME kibana-4.0.2-linux-x64

# Grab gosu for easy step-down from root
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture)" \
    && curl -o /usr/local/bin/gosu.asc -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture).asc" \
    && gpg --verify /usr/local/bin/gosu.asc \
    && rm /usr/local/bin/gosu.asc \
    && chmod +x /usr/local/bin/gosu

# Install Kibana.
RUN cd /opt && \
    wget https://download.elasticsearch.org/kibana/kibana/$KIBANA_PKG_NAME.tar.gz && \
    tar -xzvf $KIBANA_PKG_NAME.tar.gz && \
    rm $KIBANA_PKG_NAME.tar.gz && \
    mv $KIBANA_PKG_NAME kibana

# Add kibana to PATH.
ENV PATH /opt/kibana/bin:$PATH

# Mount kibana.yml config.
COPY config /opt/kibana/config

COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["kibana"]