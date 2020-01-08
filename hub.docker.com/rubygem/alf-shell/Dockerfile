FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.16.4

RUN gem install alf-shell --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["alf"]
CMD ["--help"]
