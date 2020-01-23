FROM ruby:2.4

LABEL maintainer="trung.n.k@gmail.com"
LABEL description="Vanilla cfn_nag runtime without built-in rules"

WORKDIR /tmp
COPY cfn_nag/ .
RUN gem build cfn-nag.gemspec
RUN gem install cfn-nag*.gem
