FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9

RUN gem install ctioga2 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ctioga2"]
CMD ["--help"]
