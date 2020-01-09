FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.7

RUN gem install apu --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["apu"]
CMD ["--help"]
