FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.0

RUN gem install fs_template --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fs_template"]
CMD ["--help"]
