FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.1.9

RUN gem install ar_mailer_rails3 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ar_sendmail_rails3"]
CMD ["--help"]
