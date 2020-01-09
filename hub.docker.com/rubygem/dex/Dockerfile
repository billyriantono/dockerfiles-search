FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.4

RUN gem install Dex --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["Dex"]
CMD ["--help"]
