FROM alpine:3.10.2

ENV PORT=1234

RUN apk --no-cache add socat

VOLUME /var/run/docker.sock
EXPOSE ${PORT}

CMD socat TCP-LISTEN:${PORT},reuseaddr,fork UNIX-CLIENT:/var/run/docker.sock

