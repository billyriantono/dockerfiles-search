FROM alpine:latest

RUN apk add --update --no-cache curl jq coreutils

COPY dockertags.sh /
RUN chmod +x /dockertags.sh

ENTRYPOINT ["/dockertags.sh"]
