FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.3

RUN gem install c_project --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["c_project"]
CMD ["--help"]
