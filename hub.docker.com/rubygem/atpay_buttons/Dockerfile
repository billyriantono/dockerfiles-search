FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0.0

RUN gem install atpay_buttons --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["atpay_buttons"]
CMD ["--help"]
