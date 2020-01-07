FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.3

RUN gem install gls_agent --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gls_create_label"]
CMD ["--help"]
