FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.0

RUN gem install cosmo --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cosmo"]
CMD ["--help"]
