FROM ruby:2.2.2-slim
MAINTAINER mactynow

ENV NEW_RELIC_DEBUG verbose

WORKDIR .
COPY Gemfile Gemfile
COPY Gemfile.lock Gemfile.lock
RUN bundle install

RUN rm -rf /tmp/*
ADD nrsysmond /
ADD nrsysmond.sh /

CMD etcd-env /global ./nrsysmond.sh