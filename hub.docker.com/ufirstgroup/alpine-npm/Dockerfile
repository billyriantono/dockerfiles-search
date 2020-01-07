FROM mhart/alpine-node:7.10.0

MAINTAINER Jean-Luc Geering <jeanluc.geering@ufirstgroup.com>

# install bash, su-exec and tini

RUN apk update && apk upgrade && apk add \
  bash \
  su-exec \
  tini

USER root

WORKDIR "/workdir"

ENV WORKDIR "/workdir"
ENV HOMEDIR "/homedir"

VOLUME ["/workdir", "/homedir"]

COPY entrypoint.sh /

ENTRYPOINT ["/sbin/tini", "--", "/entrypoint.sh"]
CMD ["npm"]
