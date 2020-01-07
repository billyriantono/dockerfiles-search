FROM alpine:latest
MAINTAINER Michael Campbell <michael.campbell@gmail.com>

RUN apk update && apk add py-pip && pip install httpie

CMD ["--help"]
ENTRYPOINT ["/usr/bin/http"]
