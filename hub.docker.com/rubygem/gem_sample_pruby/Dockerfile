FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.2

RUN gem install gem_sample_pruby --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gem_sample_pruby"]
CMD ["--help"]
