FROM debian:stretch-slim
RUN apt-get update && apt-get install wget make gcc libevent-dev perl sudo -y
RUN cd /opt \
    && wget http://memcached.org/files/old/memcached-1.4.14.tar.gz \
    && tar -zxvf memcached-1.4.14.tar.gz \
    && cd memcached-1.4.14 \
    && ./configure && make && make test && sudo make install \
    && rm -Rf /opt/*

RUN export SUDO_FORCE_REMOVE=yes ; apt-get purge -fy wget make gcc sudo --autoremove \
     && rm -Rf /var/cache/*

CMD ["memcached","-u","www-data"]

