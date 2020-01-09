FROM scratch

ADD centos7-docker.tar.xz /
RUN rm -rf /var/log/* /tmp/*

ENV container=docker LANG=en_US.UTF-8 LC_COLLATE=POSIX
STOPSIGNAL RTMIN+3
ENTRYPOINT ["/usr/sbin/init"]
