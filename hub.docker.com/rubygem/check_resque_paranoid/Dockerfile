FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.4

RUN gem install check_resque_paranoid --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["check_resque"]
CMD ["--help"]
