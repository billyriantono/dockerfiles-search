FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.2.2-x64-mingw32

RUN gem install hiera --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hiera"]
CMD ["--help"]
