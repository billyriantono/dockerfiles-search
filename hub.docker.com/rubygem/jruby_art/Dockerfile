FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.9

RUN gem install jruby_art --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["k9"]
CMD ["--help"]
