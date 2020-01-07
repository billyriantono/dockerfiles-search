FROM ruby:2.4.1-alpine

MAINTAINER Jean-Luc Geering <jeanluc.geering@ufirstgroup.com>

ENV VERSION=v8.0.0

# install bash, su-exec and tini

RUN apk update && apk upgrade && apk add \
  bash \
  su-exec \
  tini

RUN gem install rubocop

USER root

WORKDIR "/workdir"

ENV WORKDIR "/workdir"
ENV HOMEDIR "/homedir"

VOLUME ["/workdir", "/homedir"]

COPY entrypoint.sh /

ENTRYPOINT ["/sbin/tini", "--", "/entrypoint.sh"]
CMD ["rubocop"]
