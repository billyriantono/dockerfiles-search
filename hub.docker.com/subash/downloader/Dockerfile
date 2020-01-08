FROM alpine:3.9
RUN apk add --no-cache aria2
RUN adduser -D -g '' aria2
USER aria2
VOLUME [ "/downloads" ]
ENTRYPOINT [ "aria2c", "-x", "5", "--dir=/downloads", "--file-allocation=none", "--continue" ]