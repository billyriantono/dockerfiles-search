FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install facturae_print --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["facturae_print"]
CMD ["--help"]
