FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.3

RUN gem install aws-s3 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["s3sh"]
CMD ["--help"]
