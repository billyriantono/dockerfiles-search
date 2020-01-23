FROM fedora:28
MAINTAINER Alex Smith <alex.smith@redhat.com>
ENV container docker
RUN dnf install -y tor && dnf clean all
RUN systemctl enable tor.service && systemctl mask dnf-makecache.timer
STOPSIGNAL SIGRTMIN+3
EXPOSE 9050
CMD ["/sbin/init"]
