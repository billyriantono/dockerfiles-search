FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.1

RUN gem install clean_files --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["clean_files"]
CMD ["--help"]
