FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.8

RUN gem install jsonpathv2 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jsonpathv2"]
CMD ["--help"]
