FROM alpine:3.6
LABEL maintainer="gmblar+github@gmail.com"

COPY content /
RUN sshd-setup

ENTRYPOINT ["sshd-entrypoint"]
CMD ["/usr/sbin/sshd"]
