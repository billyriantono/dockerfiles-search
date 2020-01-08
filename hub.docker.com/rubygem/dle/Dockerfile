FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.1

RUN gem install dle --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dle"]
CMD ["--help"]
