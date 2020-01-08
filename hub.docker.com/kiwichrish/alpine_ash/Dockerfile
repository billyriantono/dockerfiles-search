# Alpine ash container, for testing stuff.
# Chris H <chris@trash.co.nz>

FROM alpine:latest

RUN apk add --update busybox-extras mariadb-client openssh-client tzdata nmap tcpdump && rm -f /var/cache/apk/*

CMD ["/bin/ash"]
