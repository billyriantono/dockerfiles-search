FROM ubuntu:14.04

ENV MESOSDNS_VERSION  v0.6.0

RUN set -x \
    && apt-get update --quiet \
    && apt-get install --quiet --yes --no-install-recommends wget curl \
    && apt-get clean \
    && mkdir -p /mesos-dns \
    && wget https://github.com/mesosphere/mesos-dns/releases/download/${MESOSDNS_VERSION}/mesos-dns-${MESOSDNS_VERSION}-linux-amd64 -O /mesos-dns/run --no-check-certificate \
    && chmod 0755 /mesos-dns/run

WORKDIR /mesos-dns

COPY "start.sh" "/mesos-dns/start.sh"
ENTRYPOINT ["/mesos-dns/start.sh"]
