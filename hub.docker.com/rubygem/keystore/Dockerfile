FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=KeyStore-0.0.1

RUN gem install keystore --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["keystore.rb"]
CMD ["--help"]
