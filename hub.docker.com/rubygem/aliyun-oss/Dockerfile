FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.7.0.1397365150

RUN gem install aliyun-oss --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["oss"]
CMD ["--help"]
