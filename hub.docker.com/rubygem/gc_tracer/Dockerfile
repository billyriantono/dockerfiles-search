FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.5.1

RUN gem install gc_tracer --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["objspace_recorder_convert.rb"]
CMD ["--help"]
