FROM martinussuherman/alpine-tz-ep

ENV LABEL_MAINTAINER="Martinus Suherman" \
    LABEL_VENDOR="martinussuherman" \
    LABEL_IMAGE_NAME="martinussuherman/alpine-tz-ep-pound" \
    LABEL_URL="https://hub.docker.com/r/martinussuherman/alpine-tz-ep-pound/" \
    LABEL_VCS_URL="https://github.com/martinussuherman/alpine-tz-ep-pound" \
    LABEL_DESCRIPTION="Docker image for Pound, based on Alpine Linux." \
    LABEL_LICENSE="GPL-3.0" \
    # container/su-exec UID \
    EUID=9999 \
    # container/su-exec GID \
    EGID=9999 \
    # container/su-exec user name \
    EUSER=pound \
    # container/su-exec group name \
    EGROUP=pound \
    # container user home dir \
    EHOME=/etc/pound

RUN apk add --no-cache pound \
    && mkdir /etc/pound \
    && mkdir /etc/pound/certs \
    && mkdir /var/run/pound 

ENTRYPOINT ["/entrypoint_exec.sh", "pound"]

ARG LABEL_VERSION="latest"
ARG LABEL_BUILD_DATE
ARG LABEL_VCS_REF

# Build-time metadata as defined at http://label-schema.org
LABEL maintainer=$LABEL_MAINTAINER \
      org.label-schema.build-date=$LABEL_BUILD_DATE \
      org.label-schema.description=$LABEL_DESCRIPTION \
      org.label-schema.name=$LABEL_IMAGE_NAME \
      org.label-schema.schema-version="1.0" \
      org.label-schema.url=$LABEL_URL \
      org.label-schema.license=$LABEL_LICENSE \
      org.label-schema.vcs-ref=$LABEL_VCS_REF \
      org.label-schema.vcs-url=$LABEL_VCS_URL \
      org.label-schema.vendor=$LABEL_VENDOR \
      org.label-schema.version=$LABEL_VERSION
