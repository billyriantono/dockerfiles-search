FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.3

RUN gem install grntest --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["grntest"]
CMD ["--help"]
