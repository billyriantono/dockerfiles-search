FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.3

RUN gem install cft_smartcloud --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cft_smartcloud"]
CMD ["--help"]
