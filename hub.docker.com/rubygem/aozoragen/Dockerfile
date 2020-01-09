FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.5

RUN gem install aozoragen --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["aozora2pdf"]
CMD ["--help"]
