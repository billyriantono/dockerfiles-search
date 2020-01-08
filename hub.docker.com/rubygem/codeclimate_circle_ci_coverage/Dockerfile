FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.2

RUN gem install codeclimate_circle_ci_coverage --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["report_coverage"]
CMD ["--help"]
