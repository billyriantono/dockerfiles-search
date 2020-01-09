FROM ypcs/debian:buster

RUN /usr/lib/docker-helpers/apt-setup && \
    /usr/lib/docker-helpers/apt-upgrade && \
    apt-get --assume-yes install \
        apt-cacher-ng && \
    /usr/lib/docker-helpers/apt-cleanup

CMD ["pidfile=/var/run/apt-cacher-ng.pid", "foreground=1", "SocketPath=/var/run/apt-cacher-ng.socket"]
ENTRYPOINT ["/usr/sbin/apt-cacher-ng"]
