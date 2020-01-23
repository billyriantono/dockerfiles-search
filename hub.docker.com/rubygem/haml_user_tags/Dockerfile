FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.3

RUN gem install haml_user_tags --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hamlut"]
CMD ["--help"]
