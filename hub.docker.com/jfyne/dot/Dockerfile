FROM alpine

RUN apk add --no-cache graphviz font-noto

RUN adduser -S dot
USER dot

ENTRYPOINT ["/usr/bin/dot"]
