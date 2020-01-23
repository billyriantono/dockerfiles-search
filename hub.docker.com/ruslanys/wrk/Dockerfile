FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=4.1.0.beta.1

RUN gem install haml --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["haml"]
CMD ["--help"]
