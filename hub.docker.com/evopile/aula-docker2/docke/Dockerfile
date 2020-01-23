FROM alpine

ENV PACKAGES="\
  py-pip \
  jq \
"

RUN apk add --update $PACKAGES \
  && pip install yq \
  && rm /var/cache/apk/*

COPY ./go.sh /
ENTRYPOINT ["/go.sh"]
CMD []
