FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.9

RUN gem install httpit --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["httpit"]
CMD ["--help"]
