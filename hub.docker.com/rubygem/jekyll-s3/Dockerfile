FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.2.0

RUN gem install jekyll-s3 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jekyll-s3"]
CMD ["--help"]
