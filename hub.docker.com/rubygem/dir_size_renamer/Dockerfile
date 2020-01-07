FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install dir_size_renamer --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dir_size_renamer"]
CMD ["--help"]
