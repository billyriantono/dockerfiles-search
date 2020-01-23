FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.2

RUN gem install jenkins_job --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jenkins_job"]
CMD ["--help"]
