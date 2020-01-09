FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.4.3

RUN gem install heroku_hatchet --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hatchet"]
CMD ["--help"]
