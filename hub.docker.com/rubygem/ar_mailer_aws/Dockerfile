FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.0

RUN gem install ar_mailer_aws --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ar_mailer_aws"]
CMD ["--help"]
