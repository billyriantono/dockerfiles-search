FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.1

RUN gem install count_von_count --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["count_von_count"]
CMD ["--help"]
