FROM ruby:2.4

MAINTAINER aspgems

ENV RUBOCOP_VERSION=0.48.1

RUN gem install rubocop --version ${RUBOCOP_VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["rubocop"]
CMD ["--help"]

