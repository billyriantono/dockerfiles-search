FROM ruby:2.4-alpine

LABEL org.label-schema.maintainer="EUIGS Release Team <release@euigs.com>" \
      org.label-schema.vendor="EUIGS" \
      org.label-schema.url="https://github.com/a-eperez/docker-r10k" \
      org.label-schema.name="r10k" \
      org.label-schema.license="Apache-2.0" \
      org.label-schema.vcs-url="https://github.com/a-eperez/docker-r10k" \
      org.label-schema.schema-version="1.0" \
      org.label-schema.dockerfile="/Dockerfile"

RUN apk add --update --no-cache \
    openssh-client \
    git \
    curl
RUN mkdir -m 600 -p ~/.ssh
RUN gem install -uN --clear-sources r10k

ENTRYPOINT ["r10k"]
CMD [ "--help" ]
