FROM opensuse:42.1
MAINTAINER Thomas Boerger <thomas@webhippie.de>

RUN zypper -n ref && \
  zypper -n up --skip-interactive --no-recommends && \
  zypper -n install -l --no-recommends \
    ca-certificates \
    bash \
    bash-completion \
    vim \
    curl \
    which \
    cronie \
    aaa_base && \
  zypper clean && \
  rm -rf /var/cache/zypp/*

ADD rootfs /

ENV CRON_ENABLED false
ENV TERM xterm
ENTRYPOINT ["/usr/bin/entrypoint"]
CMD ["bash"]

ARG VERSION
ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.version=$VERSION
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-ref=$VCS_REF
LABEL org.label-schema.vcs-url="https://github.com/dockhippie/opensuse.git"
LABEL org.label-schema.name="openSUSE"
LABEL org.label-schema.vendor="Thomas Boerger"
LABEL org.label-schema.schema-version="1.0"
