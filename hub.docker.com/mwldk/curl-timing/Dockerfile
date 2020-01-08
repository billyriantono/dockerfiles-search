FROM alpine:3.9

RUN apk add --no-cache curl

ADD timingoutput.json /

ENTRYPOINT ["/usr/bin/curl", "--write-out", "@timingoutput.json", "--silent", "--output", "/dev/null"]