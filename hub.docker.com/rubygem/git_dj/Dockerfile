FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install git_dj --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gdj"]
CMD ["--help"]
