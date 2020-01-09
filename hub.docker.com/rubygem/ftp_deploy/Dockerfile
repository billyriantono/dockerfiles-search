FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install ftp_deploy --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ftp_deploy"]
CMD ["--help"]
