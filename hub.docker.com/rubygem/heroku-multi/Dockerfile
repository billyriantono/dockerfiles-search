FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.1

RUN gem install heroku-multi --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["heroku-multi"]
CMD ["--help"]
