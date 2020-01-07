FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2

RUN gem install centostrano --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["centify"]
CMD ["--help"]
