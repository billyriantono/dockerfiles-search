FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.2

RUN gem install ar2gostruct --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ar2gostruct"]
CMD ["--help"]
