FROM alpine:latest as build

RUN apk add --no-cache strace

FROM scratch
WORKDIR /
ENTRYPOINT []
COPY --from=build /usr/bin/strace /usr/bin/strace

