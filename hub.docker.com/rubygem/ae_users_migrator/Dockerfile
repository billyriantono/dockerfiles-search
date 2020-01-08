FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.6

RUN gem install ae_users_migrator --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["export_ae_users"]
CMD ["--help"]
