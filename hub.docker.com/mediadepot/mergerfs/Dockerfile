FROM ubuntu:16.04

ADD https://github.com/trapexit/mergerfs/releases/download/2.23.0/mergerfs_2.23.0.ubuntu-trusty_amd64.deb /tmp/mergerfs.deb
COPY ./entrypoint /entrypoint

RUN chmod +x /entrypoint && dpkg -i /tmp/mergerfs.deb && rm /tmp/mergerfs.deb

ENTRYPOINT ["/entrypoint"]

HEALTHCHECK CMD mountpoint /media/storage
