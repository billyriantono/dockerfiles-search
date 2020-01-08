FROM walm/base:0.1.1
MAINTAINER Andreas Wålm "andreas@walm.net"

RUN \
  echo "# Installing redis" ;\
  apt-get update -qq ;\
  apt-get install -qq -y software-properties-common ;\
  add-apt-repository -y ppa:rwky/redis ;\
  apt-get update -qq ;\
  apt-get -y install redis-server ;\
  echo "vm.overcommit_memory = 1" >> /etc/sysctl.conf ;\
  \
  echo "# Clean up" ;\
  apt-get remove -qq -y software-properties-common ;\
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /setup /build

ADD redis.sh /etc/service/redis/run

EXPOSE 6379
