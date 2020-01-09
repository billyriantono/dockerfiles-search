FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install boinc_drone --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["boinc_drone"]
CMD ["--help"]
