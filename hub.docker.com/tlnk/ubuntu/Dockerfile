
FROM ubuntu:16.04
MAINTAINER MAINTAINER tlnk <support@tlnk.fr>

ARG VERSION
ARG BUILD_DATE
ARG VCS_REF

RUN apt-get update -y && \
  apt-get upgrade -y && \
  apt-get install -y \
    nano \
    wget \
    curl \
    apt-utils \
    unzip && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["bash"]

LABEL org.label-schema.version=$VERSION
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-ref=$VCS_REF
LABEL org.label-schema.vcs-url="https://github.com/tle06/ubuntu.git"
LABEL org.label-schema.name="Ubuntu"
LABEL org.label-schema.vendor="TLNK"
LABEL org.label-schema.schema-version="1.0"