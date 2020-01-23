FROM alpine

LABEL maintainer="Bjoern Stierand <bjoern-github@innovention.de>"

RUN apk upgrade \
  && apk add aria2 \
  && adduser --uid 1000 --ingroup users --disabled-password aria2
USER aria2
ENTRYPOINT ["/usr/bin/aria2c","-d","/downloads"]
