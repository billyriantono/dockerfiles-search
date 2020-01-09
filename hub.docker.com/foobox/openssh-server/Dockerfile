ARG ARCH=amd64
ARG ALPINE_VERSION=3.8
FROM $ARCH/alpine:$ALPINE_VERSION

ARG BUILD_DATE
ARG VCS_URL
ARG VCS_REF
LABEL org.label-schema.schema-version=1.0
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-ref=$VCS_REF
LABEL org.label-schema.vcs-url=$VCS_URL
LABEL maintainer="Andreas Treichel <gmblar+github@gmail.com>"

ARG OPENSSH_SERVER_VERSION=7.7
EXPOSE 22/tcp
COPY src /
RUN openssh-setup
HEALTHCHECK CMD openssh-healthcheck
ENTRYPOINT ["openssh-entrypoint"]
CMD ["/usr/sbin/sshd", "-D", "-e"]
