FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.2

RUN gem install full_lengther_next --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["plot_taxonomy.rb"]
CMD ["--help"]
