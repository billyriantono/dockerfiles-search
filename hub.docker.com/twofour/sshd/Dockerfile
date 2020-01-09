FROM alpine:3.8

ARG SSHD_VERSION=7.7
EXPOSE 22/tcp
COPY src /
RUN sshd-setup
ENTRYPOINT ["sshd-entrypoint"]
CMD ["/usr/sbin/sshd"]
