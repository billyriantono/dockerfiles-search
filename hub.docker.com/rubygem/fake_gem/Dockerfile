FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.9

RUN gem install fake_gem --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fake_gem"]
CMD ["--help"]
