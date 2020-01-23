FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.3.2

RUN gem install Html2Feedbooks --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["html2fb.rb"]
CMD ["--help"]
