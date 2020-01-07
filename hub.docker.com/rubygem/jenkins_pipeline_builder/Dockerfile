FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.4

RUN gem install jenkins_pipeline_builder --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["generate"]
CMD ["--help"]
