FROM ubuntu:18.04

ENV NZBHYDRA2_VERSION=2.5.5

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get -q update && \
  apt-get upgrade -y && \
  apt-get install openjdk-8-jre-headless unzip wget dumb-init -y -q --no-install-recommends && \
  rm -rf /tmp/* /var/lib/apt/lists/* /var/tmp/*
RUN mkdir /opt/nzbhydra2 /data/ && \
  wget -q https://github.com/theotherp/nzbhydra2/releases/download/v${NZBHYDRA2_VERSION}/nzbhydra2-${NZBHYDRA2_VERSION}-linux.zip -O /tmp/nzbhydra2.zip && \
  unzip /tmp/nzbhydra2.zip -d /opt/nzbhydra2 && \
  chmod 700 /opt/nzbhydra2/nzbhydra2 /data/ && \
  rm -f /tmp/nzbhydra2.zip

EXPOSE 8080
VOLUME [ "/data" ]

ENTRYPOINT [ "/usr/bin/dumb-init" ]
CMD ["/opt/nzbhydra2/nzbhydra2", "--nobrowser", "--datafolder", "/data/", "--port", "8080"]
