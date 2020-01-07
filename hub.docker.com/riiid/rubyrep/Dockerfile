FROM ruby:1.9.3
MAINTAINER han@riiid.co

ADD . /rubyrep

WORKDIR /rubyrep

RUN gem build /rubyrep/rubyrep.gemspec && gem install rubyrep-1.2.1.2013010901.gem activerecord-postgresql-adapter --no-ri --no-rdoc

CMD rubyrep replicate -c /rubyrep/myrubyrep.conf
