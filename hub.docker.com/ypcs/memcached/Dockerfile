FROM ypcs/debian:stretch

RUN \
    /usr/local/sbin/docker-upgrade && \
    apt-get --assume-yes install \
        memcached && \
    /usr/local/sbin/docker-cleanup

CMD ["/usr/bin/memcached", "-m", "64", "-p" ,"11211", "-u", "memcache", "-l", "127.0.0.1"]
