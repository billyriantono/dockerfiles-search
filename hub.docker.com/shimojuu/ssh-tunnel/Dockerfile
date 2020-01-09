FROM alpine:3.8

RUN apk --no-cache add autossh

EXPOSE 2222

ENTRYPOINT ["/usr/bin/autossh", "-M", "0", "-T", "-N", "-oStrictHostKeyChecking=no", "-oServerAliveInterval=30", "-oUserKnownHostsFile=/dev/null", "-L"]
