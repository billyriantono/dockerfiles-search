FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.2

RUN gem install gorgyrella --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gorgyrella"]
CMD ["--help"]
