FROM alpine:latest

RUN apk -v --update --no-cache add \
        git \
        openssh

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.docker.dockerfile=Dockerfile \
      org.label-schema.license=LGPL \
      org.label-schema.name=git \
      org.label-schema.version=$VERSION \
      org.label-schema.url=https://gitlab.com/madhead-docker/git \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url=https://gitlab.com/madhead-docker/git.git \
      org.label-schema.vcs-type=git
