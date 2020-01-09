FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.1

RUN gem install batch_manager --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["bm_exec"]
CMD ["--help"]
