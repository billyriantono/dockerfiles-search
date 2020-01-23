FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.2

RUN gem install gitme_time --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gitme_time"]
CMD ["--help"]
