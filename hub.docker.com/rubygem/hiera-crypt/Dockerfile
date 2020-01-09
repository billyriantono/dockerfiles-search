FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3

RUN gem install hiera-crypt --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hiera-crypt"]
CMD ["--help"]
