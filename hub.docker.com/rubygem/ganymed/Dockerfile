FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.2

RUN gem install ganymed --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ganymed"]
CMD ["--help"]
