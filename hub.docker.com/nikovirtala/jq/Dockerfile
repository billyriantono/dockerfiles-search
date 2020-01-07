FROM alpine:edge
LABEL maintainer "Niko Virtala <niko@nikovirtala.io>"

RUN apk add --no-cache --virtual curl ca-certificates && \
  curl -sSLO https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 && \
	chmod +x jq-linux64 && \
  mv jq-linux64 /usr/local/bin/jq

RUN adduser -D -g '' -h /home/nikovirtala nikovirtala
USER nikovirtala
WORKDIR /home/nikovirtala

ENTRYPOINT ["jq"]
