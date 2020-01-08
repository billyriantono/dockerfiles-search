FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.4

RUN gem install adamwiggins-rest-client --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["restclient"]
CMD ["--help"]
