FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.2.0

RUN gem install axtro-ar_mailer --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ar_sendmail"]
CMD ["--help"]
