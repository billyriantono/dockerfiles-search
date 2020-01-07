FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.2

RUN gem install douban_fm_hotkey --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["douban_fm_hotkey"]
CMD ["--help"]
