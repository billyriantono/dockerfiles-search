FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=10.8.27.1

RUN gem install home_cleaner --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["home_cleaner"]
CMD ["--help"]
