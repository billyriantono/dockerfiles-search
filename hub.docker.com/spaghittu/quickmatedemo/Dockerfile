FROM alpine

ENV NAME=QuickMate-Demo
ADD ./build /build
ADD ./entrypoint /entrypoint

RUN apk --no-cache add bash

RUN bash < /entrypoint

