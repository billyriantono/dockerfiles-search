FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.1

RUN gem install imgur2 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["imgur2"]
CMD ["--help"]
