FROM alpine
LABEL maintainer "Alex Haydock <alex@alexhaydock.co.uk>"

RUN apk --no-cache add smartmontools

ENTRYPOINT ["/usr/sbin/smartctl"]