# Python v3.5.1
# docker run --rm takatakato/python:3.5

FROM alpine:3.4

RUN apk --no-cache add python3 \
    && ln -sf /usr/bin/python3.5 /usr/bin/python

CMD ["/usr/bin/python", "--version"]