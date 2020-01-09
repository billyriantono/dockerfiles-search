FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.46

RUN gem install cloudfuji --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cloudfuji"]
CMD ["--help"]
