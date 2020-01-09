FROM alpine:latest

RUN apk --no-cache add socat

EXPOSE 2375/tcp

ENTRYPOINT ["socat", "TCP-LISTEN:2375,fork,reuseaddr", "UNIX:/var/run/docker.sock"]
