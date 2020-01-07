FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.2

RUN gem install android_lint_translate_checkstyle_format --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["android_lint_translate_checkstyle_format"]
CMD ["--help"]
