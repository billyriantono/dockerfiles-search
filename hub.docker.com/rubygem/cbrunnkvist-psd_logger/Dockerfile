FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.5

RUN gem install cbrunnkvist-psd_logger --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["psd_logger"]
CMD ["--help"]
