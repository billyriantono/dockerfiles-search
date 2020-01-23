FROM debian:jessie

RUN apt-get update && apt-get install --no-install-recommends -y \
    curl \
    ca-certificates \
    make \
    git-core

RUN curl -s https://storage.googleapis.com/golang/go1.3.1.linux-amd64.tar.gz | tar -v -C /usr/local -xz
ENV PATH $PATH:/usr/local/go/bin:/go/bin

ADD types.db /
ADD run.sh /
 
RUN git clone https://github.com/hoonmin/influxdb-collectd-proxy.git && \
    make -C /influxdb-collectd-proxy

USER 1
EXPOSE 8096
ENTRYPOINT ["/run.sh"]
