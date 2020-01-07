FROM ruby:2.2

MAINTAINER Ron Kurr <kurr@jvmguy.com>

COPY newrelic_mongodb_agent-2.4.6 /opt/example

WORKDIR /opt/example

RUN ["bundle","install"]

ENTRYPOINT ["./newrelic_mongodb_agent"]

