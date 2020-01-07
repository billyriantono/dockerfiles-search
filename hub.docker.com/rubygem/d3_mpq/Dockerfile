FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.2

RUN gem install d3_mpq --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["d3_mpq"]
CMD ["--help"]
