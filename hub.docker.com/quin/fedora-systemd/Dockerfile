# See https://developers.redhat.com/blog/2016/09/13/running-systemd-in-a-non-privileged-container/ for details

FROM fedora:26
ENV container docker
STOPSIGNAL SIGRTMIN+3
ENTRYPOINT [ "/sbin/init" ]
