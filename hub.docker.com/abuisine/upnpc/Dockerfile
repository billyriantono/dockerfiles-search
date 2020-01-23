FROM alpine:3.7

LABEL maintainer="Alexandre Buisine <alexandrejabuisine@gmail.com>" version="1.0"

RUN apk add --no-cache miniupnpc

ENTRYPOINT ["/usr/bin/upnpc"]
CMD ["-s"]