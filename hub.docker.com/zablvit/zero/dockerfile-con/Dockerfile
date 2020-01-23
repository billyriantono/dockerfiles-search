FROM ypcs/debian:stretch

RUN /usr/local/sbin/docker-upgrade && \
    apt-get --assume-yes install \
        tor && \
    /usr/local/sbin/docker-cleanup

