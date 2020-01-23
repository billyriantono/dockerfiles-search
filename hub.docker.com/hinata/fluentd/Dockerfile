#@# vim: set filetype=dockerfile:
FROM fluent/fluentd:v1.7.4-1.0
MAINTAINER Takahiro INOUE <takahiro.inoue@aist.go.jp>

USER root

RUN gem install -N fluent-plugin-slack --version 0.6.7

USER fluent
