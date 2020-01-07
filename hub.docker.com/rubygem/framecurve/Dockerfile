FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.2.2

RUN gem install framecurve --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["framecurve_from_fcp_xml"]
CMD ["--help"]
