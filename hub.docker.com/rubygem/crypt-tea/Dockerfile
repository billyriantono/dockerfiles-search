FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.3.0

RUN gem install crypt-tea --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["xxtea"]
CMD ["--help"]
