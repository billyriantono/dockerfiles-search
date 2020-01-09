FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.3

RUN gem install client_for_poslynx --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fake_pos_terminal"]
CMD ["--help"]
