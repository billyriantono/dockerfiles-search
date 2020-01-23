FROM phusion/baseimage:0.9.16

CMD ["/usr/bin/kafka-manager"]

EXPOSE 9000

ENV \
  KM_REVISION=ac71562ef67f0eeca8d1ffe6130ef78a2c346875 \
  KM_VERSION=1.2.5

RUN \
  apt-get update && \
  apt-get install -y fakeroot git openjdk-7-jdk && \
  git clone https://github.com/yahoo/kafka-manager /tmp/kafka-manager && \
  cd /tmp/kafka-manager && \
  git checkout ${KM_REVISION} && \
  ./sbt clean debian:packageBin && \
  dpkg -i ./target/kafka-manager_${KM_VERSION}_all.deb && \
  apt-get purge -y fakeroot git && \
  apt-get autoremove -y && \
  apt-get clean && \
  rm -rf /root/.sbt /root/.ivy2 /tmp/* /var/lib/apt/lists/* /var/tmp/*
