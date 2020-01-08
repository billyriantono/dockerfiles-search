FROM docker/compose:1.23.1

ENV PACKAGES="\
  py-pip \
  jq \
"

RUN apk add --update $PACKAGES \
  && pip install yq \
  && rm /var/cache/apk/*
