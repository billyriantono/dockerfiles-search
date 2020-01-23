FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.5

RUN gem install html2pdf --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["html2pdf"]
CMD ["--help"]
