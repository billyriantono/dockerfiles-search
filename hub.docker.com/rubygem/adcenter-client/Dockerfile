FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=8.0.3

RUN gem install adcenter-client --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["get_adcenter_account_info.rb"]
CMD ["--help"]
